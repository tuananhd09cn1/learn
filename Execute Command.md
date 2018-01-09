@Component
@Transactional
public class AnalysisTask {
	
	private final Logger log = LoggerFactory.getLogger(AnalysisTask.class);
	
	public AnalysisTask() {
	}

	
	@Async("analysisTaskExecutor")
	public void run(AnalysisDTO ana) {
		
		Report report = new Report();
		report.setCodeDiff(codeDiffRepository.findOne(ana.getCodeDiffId()));
		report.setAppModel(ana.getModel() == null ? null : modelRepository.findByName(ana.getModel()));
		report.setModule(ana.getModule() == null ? null : moduleRepository.findByNameAndAppModel(ana.getModule(), report.getAppModel()));
		report.setVersion(report.getCodeDiff().getTargetVersion());
		
		report = reportRepository.save(report);
		
		try {
			
			boolean isWindows = System.getProperty("os.name")
					  .toLowerCase().startsWith("windows");
			
			ProcessBuilder builder = new ProcessBuilder();
			
			if (isWindows) {
			    builder.command("cmd.exe", "/c", 
			    		"java -jar " +  ana.getJar() + 
			    		" -model " +  ana.getModel() + 
			    		" -module " + ana.getModule() + 
			    		" -v1 " + ana.getV1() + 
			    		" -v2 " + ana.getV2() + 
			    		" -static " + ana.getStaticFile() + 
			    		" -dynamic " + ana.getDynamicDirectory() + 
			    		" -reportId " + report.getId() + 
			    		" -transferServer -debug");
			} else {
			    builder.command("sh", "-c", 
			    		"java -jar " +  ana.getJar() + 
			    		" -model " +  ana.getModel() + 
			    		" -module " + ana.getModule() + 
			    		" -v1 " + ana.getV1() + 
			    		" -v2 " + ana.getV2() + 
			    		" -static " + ana.getStaticFile() + 
			    		" -dynamic " + ana.getDynamicDirectory() + 
			    		" -reportId " + report.getId() + 
			    		" -transferServer -debug");
			}
			
			builder.directory(new File(directory));
			log.debug("java -jar " +  ana.getJar() + 
		    		" -model " +  ana.getModel() + 
		    		" -module " + ana.getModule() + 
		    		" -v1 " + ana.getV1() + 
		    		" -v2 " + ana.getV2() + 
		    		" -static " + ana.getStaticFile() + 
		    		" -dynamic " + ana.getDynamicDirectory() + 
		    		" -reportId " + report.getId() + 
		    		" -transferServer -debug");
			
			Process process = builder.start();
			
			try {
				StreamGobbler streamGobbler = 
				  new StreamGobbler(process.getInputStream(), System.out::println);
				
				Executors.newSingleThreadExecutor().submit(streamGobbler);
			} catch (Exception e) {
				// TODO: handle exception
			}
			
			int exitCode = -1;
			exitCode = process.waitFor();
			
			log.debug("Exit code: {}", exitCode);
			
		} catch (Exception e) {
			e.printStackTrace();
			throw new InternalServerException();
		}
	}
}

------
@Configuration
@EnableAsync
@EnableScheduling
public class ThreadConfiguration {
	
	@Value(value="${spring.maxqueuesize}")
	private int maxQueueSize;
	
	@Value(value="${spring.maxpoolsize}")
	private int maxPoolSize;

	
	@Bean(name="analysisTaskExecutor")
	public ExecutorService analysisExecutor() {
		
		ExecutorService exe = new ThreadPoolExecutor(10, maxPoolSize, 0L, TimeUnit.MILLISECONDS,   
				  new LinkedBlockingQueue<Runnable>(maxQueueSize));
		
		return exe;
	}

}
-----
@Autowired
	private DiffCodeTask diffCodeTask;

	@Autowired
	@Qualifier("diffTaskExecutor")
	private ExecutorService executorService;

	@Override
	public CodeDiff createReport(ReportDTO reportDTO) {

		
		try {
			ThreadPoolExecutor executor = (ThreadPoolExecutor) executorService;
			log.debug("Current active inject thread size: {}", executor.getPoolSize());
			log.debug("Current inject remain queue size: {}", executor.getQueue().remainingCapacity());
			if (executor.getQueue().remainingCapacity() < 1)
				throw new BadRequestException("Queue is full, please wait a couple minutes and try again.");

			diffCodeTask.run(d);
		} catch (Exception e) {
			// TODO: handle exception
			e.printStackTrace();
			throw new BadRequestException("Queue is full, please wait a couple minutes and try again.");
		}

		return codeDiff;
	}
