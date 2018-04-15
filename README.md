https://gitlab.com/gitlab-examples/ssh-private-key
package com.bigqsys.ad.yt;

import java.io.FileOutputStream;

import com.voicerss.tts.AudioCodec;
import com.voicerss.tts.AudioFormat;
import com.voicerss.tts.Languages;
import com.voicerss.tts.SpeechDataEvent;
import com.voicerss.tts.SpeechDataEventListener;
import com.voicerss.tts.SpeechErrorEvent;
import com.voicerss.tts.SpeechErrorEventListener;
import com.voicerss.tts.VoiceParameters;
import com.voicerss.tts.VoiceProvider;

public class Example {
///*	   public static void main (String args[]) throws Exception {
//	        VoiceProvider tts = new VoiceProvider("df852440cfc54e92b425fcb156dcf39f");
//			
//	        VoiceParameters params = new VoiceParameters("Hello, world!", Languages.English_UnitedStates);
//	        params.setCodec(AudioCodec.WAV);
//	        params.setFormat(AudioFormat.Format_44KHZ.AF_44khz_16bit_stereo);
//	        params.setBase64(false);
//	        params.setSSML(false);
//	        params.setRate(0);
//			
//	        byte[] voice = tts.speech(params);
//			
//	        FileOutputStream fos = new FileOutputStream("voice.mp3");
//	        fos.write(voice, 0, voice.length);
//	        fos.flush();
//	        fos.close();
//	    }*/
	   public static void main (String args[]) throws Exception {
	        VoiceProvider tts = new VoiceProvider("df852440cfc54e92b425fcb156dcf39f");
			
	        VoiceParameters params = new VoiceParameters("Hello, world!", Languages.English_UnitedStates);
	        params.setCodec(AudioCodec.WAV);
	        params.setFormat(AudioFormat.Format_44KHZ.AF_44khz_16bit_stereo);
	        params.setBase64(false);
	        params.setSSML(false);
	        params.setRate(0);
			
	        tts.addSpeechErrorEventListener(new SpeechErrorEventListener() {
	            @Override
	            public void handleSpeechErrorEvent(SpeechErrorEvent e) {
	                System.out.print(e.getException().getMessage());
	            }
	        });
			
	        tts.addSpeechDataEventListener(new SpeechDataEventListener() {
	            @Override
	            public void handleSpeechDataEvent(SpeechDataEvent e) {
	                try {
	                    byte[] voice = (byte[])e.getData();
						
	                    FileOutputStream fos = new FileOutputStream("voice.mp3");
	                    fos.write(voice, 0, voice.length);
	                    fos.flush();
	                    fos.close();
	                } catch (Exception ex) {
	                    ex.printStackTrace();
	                }
	            }
	        });
			
	        tts.speechAsync(params);
	    }
}
//http://www.voicerss.org/sdk/java.aspx


https://github.com/sathomas/acc-wizard

http://techlaboratory.net/demos/SmartWizard4/examples/smartwizard-ajax.html#step-2
http://www.jquery-steps.com/Examples

https://www.vertex42.com/ExcelTemplates/project-planner-template.html

	"guzzlehttp/guzzle": "^6.3",
        "kontoulis/rabbitmq-laravel": "^2.1",
        "laravel/framework": "5.5.*",
        "laravel/tinker": "~1.0",
        "tcdent/php-restclient": "^0.1.7"
	https://github.com/mookofe/tail
<?php

namespace App\Http\Controllers;

use App\Http\Controllers\Controller;
use RestClient;
use GuzzleHttp\Client;
use Kontoulis\RabbitMQLaravel\Facades\RabbitMQ;
class SyncController extends Controller
{
    
    public function index(){
        $dataRequest = ["messageBody"=>"String","routingKey"=>"String","topic"=>"String","type"=>"String"];
        $client = new \GuzzleHttp\Client();
        $res = $client->request('POST', 'http://message.vinasao.net/api/publish/messages', ['json'=>$dataRequest]);
        echo print_r($res,true);
        echo $res->getBody();
      
    }
    public function customer(){
        $dataRequest = ["messageBody"=>"String","routingKey"=>"String","topic"=>"String","type"=>"String"];
        $client = new \GuzzleHttp\Client();
        $res = $client->request('POST', 'http://xposprod.vinasao.net/api/sync_category', ['auth'=>["big","big.dev"],'form_params'=>["customer_code"=>"AE0EE35EB68918BFE41722CD611FCAF9"]]);
        echo print_r($res,true);
        echo $res->getBody();
        $msg = [
            "key1" => "value1", 
            "key2" => "value2"
        ];         
        RabbitMQ::publishMessage($msg, "customer.abc.test");
    }
    
    
}
# learn
Fork to learn
https://www.javacodegeeks.com/2012/11/spring-3-1-loading-properties-for-xml-configuration-from-database.html
https://stackoverflow.com/questions/39847730/how-can-i-build-a-database-based-spring-boot-environment-property-source?rq=1
https://stackoverflow.com/questions/15328904/dynamically-declare-beans-at-runtime-in-spring
https://comsysto.com/blog-post/how-to-create-your-own-dynamic-bean-definitions-in-spring
https://stackoverflow.com/questions/12090406/dynamically-create-spring-beans-and-alter-properties-on-existing-beans
http://www.baeldung.com/spring-boot-custom-auto-configuration
http://blog.javaforge.net/post/31720600427/configuring-spring-based-web-application-from-database
https://github.com/pavansolapure/opencodez-samples/tree/master/quartz-demo/src/main/java/com/opencodez/quartz/jobs
package com.example.demo.rest;

import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStream;
import java.net.URL;
import java.util.HashMap;
import java.util.Map;
import java.util.Properties;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.ThreadPoolExecutor;

import org.codehaus.groovy.control.CompilationFailedException;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.amqp.core.TopicExchange;
import org.springframework.amqp.rabbit.core.RabbitTemplate;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.boot.SpringApplication;
import org.springframework.cloud.context.restart.RestartEndpoint;
import org.springframework.context.ApplicationContext;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import com.example.demo.config.PropertiesUtils;
import com.example.demo.scripts.jpython.ExampleType;
import com.example.demo.scripts.jpython.JythonFactory;
import com.example.demo.task.TaskCommand;
import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;

import groovy.lang.Binding;
import groovy.lang.GroovyShell;
import groovy.lang.Script;

@RestController
public class RestResource {
	@Autowired
	private TaskCommand taskCommand;
	private final Logger log = LoggerFactory.getLogger(RestResource.class);
	@Autowired
	@Qualifier("taskExecutor")
	private ExecutorService executorService;
	@Autowired
	private RabbitTemplate rabbitTemplate;
	@Autowired
	@Qualifier("senderTopicExchange")
	private TopicExchange topicExchange;
	@Autowired
	private ApplicationContext applicationContext;
	@Autowired
	private RestartEndpoint restartEndpoint;
	@Autowired
	private ObjectMapper objectMapper;
	@GetMapping("/task")
	public ResponseEntity<?> createTask() {

		try {
			// executor.submit(injectTask);
			ThreadPoolExecutor executor = (ThreadPoolExecutor) executorService;
			log.info("Current active inject thread size: {}", executor.getPoolSize());
			log.info("Current inject remain queue size: {}", executor.getQueue().remainingCapacity());
			if (executor.getQueue().remainingCapacity() < 1)
				throw new Exception("Queue is full, please wait a couple minutes and try again.");

			taskCommand.run();
		} catch (Exception e) {
			// TODO: handle exception
			e.printStackTrace();

		}

		return null;
	}

	@GetMapping("/jpython")
	public ResponseEntity<?> jPython() {

		try {
			// executor.submit(injectTask);
			JythonFactory factory = new JythonFactory("Example", "Example");

			ExampleType example = factory.create();
			example.say_hello();

			System.out.println("done");
		} catch (Exception e) {
			// TODO: handle exception
			e.printStackTrace();

		}

		return null;
	}

	@GetMapping("/groovyscript")
	public ResponseEntity<?> groovyScript() {
		GroovyShell shell = new GroovyShell();
		String script = "return 'hello world'";

		Object result = shell.evaluate(script);
		System.out.println(result);
		return null;
	}

	@GetMapping("/groovyscriptBinding")
	public ResponseEntity<?> groovyscriptBinding() {
		Binding binding = new Binding();
		binding.setVariable("a", 1);
		binding.setVariable("b", 2);
		GroovyShell shell = new GroovyShell(binding);

		String script = "return a + b";

		Object result = shell.evaluate(script);
		System.out.println(result);
		return null;
	}

	@GetMapping("/groovyscriptLoadScript")
	public ResponseEntity<?> groovyscriptLoadScript() throws CompilationFailedException, IOException {
		GroovyShell shell = new GroovyShell();

		URL url = Thread.currentThread().getContextClassLoader().getResource("crawl.groovy");
		final File file = new File(url.getPath());

		Script script = shell.parse(file);
		Object result = script.run();
		System.out.println(result);
		return null;
	}

	@GetMapping("/publish")
	public ResponseEntity<?> publish() throws CompilationFailedException, IOException {

		String message = String.format("Event no. %d of type '%s'", 1, "customer.test");
		rabbitTemplate.convertAndSend(topicExchange.getName(), "customer.test", "1");
		return null;
	}
	
	@GetMapping("/restart_app")
	public ResponseEntity<?> restart() throws CompilationFailedException, IOException {
		Thread thread = new Thread(new Runnable() {
		    @Override
		    public void run() {
		        restartEndpoint.invoke();
		    }
		});
		thread.setDaemon(false);
		thread.start();
		return null;
	}
	
	@GetMapping ( "/getval" ) 
    public   String   getVal ( @RequestParam ( value = "key" ,   defaultValue = "World" )   String   key ) throws JsonProcessingException   { 
		 Map < String ,   String >   mapOfKeyValue   =   new   HashMap < String ,   String > ( ) ; 
		 mapOfKeyValue . put ( key ,   PropertiesUtils . getProperty ( key ) ) ; 
		 return   objectMapper.writeValueAsString( mapOfKeyValue ) ; 
    }
	@GetMapping ( "/writePropeties" )
	public String writePropeties (){
		Properties prop = new Properties();
		OutputStream output = null;

		try {

			output = new FileOutputStream("message.properties");

			// set the properties value
			prop.setProperty("database", "localhost");
			prop.setProperty("dbuser", "mkyong");
			prop.setProperty("dbpassword", "password");

			// save properties to project root folder
			prop.store(output, null);

		} catch (IOException io) {
			io.printStackTrace();
		} finally {
			if (output != null) {
				try {
					output.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}

		}
		return "Done";
	}
}
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.example</groupId>
	<artifactId>demo</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>demo</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>1.5.9.RELEASE</version>
		<relativePath /> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
		<junit.jupiter.version>5.0.0</junit.jupiter.version>
		<junit.vintage.version>${junit.version}.0</junit.vintage.version>
		<junit.platform.version>1.0.0</junit.platform.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-actuator</artifactId>
		</dependency>
			<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter</artifactId>
			<version>1.2.4.RELEASE</version>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-amqp</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
			<scope>runtime</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
		<!-- database -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
        <dependency>
            <groupId>com.h2database</groupId>
            <artifactId>h2</artifactId>
        </dependency>
		<dependency>
			<groupId>kryonet</groupId>
			<artifactId>kryonet</artifactId>
			<version>2.21</version>
		</dependency>
		<dependency>
			<groupId>com.esotericsoftware</groupId>
			<artifactId>kryo</artifactId>
			<version>4.0.1-SNAPSHOT</version>
		</dependency>
		<dependency>
			<groupId>org.codehaus.groovy</groupId>
			<artifactId>groovy-all</artifactId>
			</dependency>
		<dependency>
			<groupId>org.jsoup</groupId>
			<artifactId>jsoup</artifactId>
			<version>1.10.2</version>
		</dependency>
		<dependency>
			<groupId>org.python</groupId>
			<artifactId>jython-standalone</artifactId>
			<version>2.5.2</version>
		</dependency>
		<!-- Added for Quartz -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-context-support</artifactId>
		</dependency>
		<dependency>
			<groupId>org.quartz-scheduler</groupId>
			<artifactId>quartz</artifactId>
			<version>2.3.0</version>
			<exclusions>
				<exclusion>
					<groupId>com.zaxxer</groupId>
					<artifactId>HikariCP-java6</artifactId>
				</exclusion>
				<exclusion>
					<groupId>com.mchange</groupId>
					<artifactId>c3p0</artifactId>
				</exclusion>
			</exclusions>
		</dependency>
		<dependency>
			<groupId>com.fasterxml.jackson.datatype</groupId>
			<artifactId>jackson-datatype-jsr310</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
			<scope>runtime</scope>
		</dependency>
		<dependency>
			<groupId>org.hsqldb</groupId>
			<artifactId>hsqldb</artifactId>
			<scope>runtime</scope>
		</dependency>
		<dependency>
			<groupId>org.projectlombok</groupId>
			<artifactId>lombok</artifactId>
			<optional>true</optional>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.junit.jupiter</groupId>
			<artifactId>junit-jupiter-api</artifactId>
			<version>${junit.jupiter.version}</version>
			<scope>test</scope>
		</dependency>
		<!-- Only required to run tests in an IDE that bundles an older version -->
		<dependency>
			<groupId>org.junit.platform</groupId>
			<artifactId>junit-platform-launcher</artifactId>
			<version>${junit.platform.version}</version>
			<scope>test</scope>
		</dependency>
		<!-- Only required to run tests in an IDE that bundles an older version -->
		<dependency>
			<groupId>org.junit.jupiter</groupId>
			<artifactId>junit-jupiter-engine</artifactId>
			<version>${junit.jupiter.version}</version>
			<scope>test</scope>
		</dependency>
		<!-- Only required to run tests in an IDE that bundles an older version -->
		<dependency>
			<groupId>org.junit.vintage</groupId>
			<artifactId>junit-vintage-engine</artifactId>
			<version>${junit.vintage.version}</version>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.scala-lang</groupId>
			<artifactId>scala-library</artifactId>
			<version>2.11.0</version>
		</dependency>
		<dependency>
			<groupId>org.scala-lang</groupId>
			<artifactId>scala-library</artifactId>
			<version>2.11.0</version>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
			<plugin>
				<artifactId>maven-surefire-plugin</artifactId>
				<configuration>
					<includes>
						<include>**/Test*.java</include>
						<include>**/*Test.java</include>
						<include>**/*Tests.java</include>
						<include>**/*TestCase.java</include>
					</includes>
					<properties>
						<!-- <includeTags>fast</includeTags> -->
						<excludeTags>slow</excludeTags>
						<!-- <configurationParameters> junit.jupiter.conditions.deactivate 
							= * </configurationParameters> -->
					</properties>
				</configuration>
				<dependencies>
					<dependency>
						<groupId>org.junit.platform</groupId>
						<artifactId>junit-platform-surefire-provider</artifactId>
						<version>${junit.platform.version}</version>
					</dependency>
				</dependencies>
			</plugin>
		</plugins>
	</build>
	<repositories>
		<repository>
			<id>sonatype-snapshots</id>
			<name>sonatype snapshots repo</name>
			<url>https://oss.sonatype.org/content/repositories/snapshots</url>
		</repository>
		<repository>
			<id>clojars</id>
			<url>http://clojars.org/repo/</url>
		</repository>
	</repositories>

</project>

