https://github.com/bramp/ffmpeg-cli-wrapper

http://www.software-testing-tutorials-automation.com/2015/03/how-to-set-proxy-settings-in-selenium.html
http://www.software-testing-tutorials-automation.com/2015/03/how-to-set-proxy-settings-in-selenium.html

https://dichvusocks.us/

https://stackoverflow.com/questions/13244181/inno-setup-app-start-when-windows-start
https://github.com/eventviva/php-image-resize
https://electronjs.org/docs/tutorial/application-distribution
https://www.mkyong.com/java/how-to-execute-shell-command-from-java/
https://github.com/codeskyblue/electron-inno-auto-update
https://coolaj86.com/articles/how-to-create-an-innosetup-installer.html
https://alvinalexander.com/java/edu/pj/pj010016
https://github.com/crilleengvall/electron-tutorial-app.git
https://gist.github.com/k4m4r82/d07cb047d26f2df4778606c48db35b14
https://research.googleblog.com/2017/06/supercharge-your-computer-vision-models.html
https://medium.com/netflix-techblog
Deep Learning for Self-Driving Cars
  /* Reset error when a new view is loaded */
		$rootScope.$on('$viewContentLoaded', function() {
			delete $rootScope.error;
		});
		
		$rootScope.initialized = true;

https://github.com/Stephn-R/electron-angular-boilerplate
# learn
Fork to learn
http://www.laptophits.com/products?price_from=0&price_to=400
The major advancements in Deep Learning in 2016
https://tryolabs.com/blog/2016/12/06/major-advancements-deep-learning-2016/
https://slack.engineering/data-wrangling-at-slack-f2e0ff633b69#.6arexm9ho
https://www.phpclasses.org/blog/post/493-php-performance-evolution.html

#http://stackoverflow.com/questions/17080494/using-grunt-server-how-can-i-redirect-all-requests-to-root-url
#http://www.williambrownstreet.net/blog/2014/04/faster-angularjs-rendering-angularjs-and-reactjs/
#TimerCheck.io
#httpProvider Angularjs

  // $locationProvider.html5Mode(true);

        /* Register error provider that shows message on failed requests or redirects to login page on
			 * unauthenticated requests */
		    $httpProvider.interceptors.push(function ($q, $rootScope, $location) {
			        return {
			        	'responseError': function(rejection) {
			        		var status = rejection.status;
			        		var config = rejection.config;
			        		var method = config.method;
			        		var url = config.url;

			        		if (status == 401) {
			        			$location.path( "/login" );
			        		} else {
			        			$rootScope.error = method + " on " + url + " failed with status " + status;
			        		}

			        		return $q.reject(rejection);
			        	}
			        };
			    }
		    );

        /* Registers auth token interceptor, auth token is either passed by header or by query parameter
         * as soon as there is an authenticated user */
        $httpProvider.interceptors.push(function ($q, $rootScope, $location) {
            return {
              'request': function(config) {
                var isRestCall = config.url.indexOf('api') >= 0;
                if (isRestCall && angular.isDefined($rootScope.accessToken)) {
                  var accessToken = $rootScope.accessToken;
                  config.headers['Authorization'] = 'Bearer '+accessToken;
                }
                return config || $q.when(config);
              }
            };
        }
      );
      $locationProvider.hashPrefix('!');
      $httpProvider.defaults.headers.common['X-Requested-With'] = 'XMLHttpRequest';
	    $httpProvider.defaults.headers.common['Accept'] = 'application/json';
      // console.log($locationProvider);
    }
]).run(['$rootScope','$cookieStore', '$location', '$window','UserServices',
 function($rootScope, $cookieStore, $location, $window,UserServices) {

  /* Reset error when a new view is loaded */
		$rootScope.$on('$viewContentLoaded', function() {
			delete $rootScope.error;
		});
    /* Try getting valid user from cookie or go to login page */
   var originalPath = $location.path();
   var accessToken = $cookieStore.get('accessToken');
   $rootScope.authenticated  = false;
   if (accessToken !== undefined) {
     $rootScope.accessToken = accessToken;
     UserServices.findMe().then(function(user) {
       $rootScope.user = user;
     });
     $rootScope.authenticated = true;
   } else {
     $location.path("/login");
   }
   $rootScope.logout = function() {
     delete $rootScope.user;
     delete $rootScope.accessToken;
     $cookieStore.remove('accessToken');
     $location.path("/login");
   };
   $rootScope.initialized = true;
}]);

https://taskboard.matthewross.me/
LayoutDirectives.directive('checkImage', function($http) {
    return {
        restrict: 'A',
        link: function(scope, element, attrs) {
            attrs.$observe('ngSrc', function(ngSrc) {
              if (ngSrc!=undefined){
                $http.get(ngSrc).success(function(){
                }).error(function(){
                  element.attr('src', 'avatar/No_image_available.svg'); // set default image
                });
              } else {
                  element.attr('src', 'avatar/No_image_available.svg'); // set default image
              }
            });
        }
    };
});
https://allotment.digital/learn/technical-seo/how-search-engines-work/indexing/
http://blog.studytube.nl/

@Controller
public class UploadController {
	private static Log log = LogFactory.getLog(UploadController.class);
    @RequestMapping(value = "/api/upload/images")
    public @ResponseBody void upload(@RequestParam("file") MultipartFile file ) throws IOException {
    	if (file!=null){
        byte[] bytes;

        if (!file.isEmpty()) {
             bytes = file.getBytes();
            //store file in storage
        }
        
        log.debug(String.format("receive from %s", file.getOriginalFilename()));
        }
    }
}

//    @Bean(name = "multipartResolver")
//    public CommonsMultipartResolver multipartResolver() {
//        CommonsMultipartResolver resolver=new CommonsMultipartResolver();
//        resolver.setDefaultEncoding("utf-8");
//        resolver.setMaxInMemorySize(5000000);
//        return resolver;
//    }

http://websystique.com/springmvc/spring-mvc-4-file-upload-example-using-commons-fileupload/
<dependency>
        	<groupId>commons-fileupload</groupId>
        	<artifactId>commons-fileupload</artifactId>
        	<version>1.3.1</version>
    	</dependency>
https://code.ciphertrick.com/2015/09/21/detect-os-browser-and-device-in-angularjs/
https://jellekralt.com/2015/08/13/dynamically-load-a-templateurl-in-an-angular-directive/
http://sharingbuttons.io/
http://dontpanic.42.nl/2015/04/cors-with-spring-mvc.html
https://support.google.com/webmasters/answer/79812
https://vmdao.wordpress.com/2016/03/21/tong-quat-ve-jpa-java-persistence-api/
http://www.martinfowler.com/articles/injection.html
https://itviec.com/it-jobs/20-developer-java-php-net-nissho-electronics-4322
http://docs.guzzlephp.org/en/latest/index.html
http://o7planning.org/en/10125/using-hibernate-tools-generate-entity-classes-from-tables

https://howtodoinjava.com/core-java/multi-threading/java-thread-pool-executor-example/
http://tutorials.jenkov.com/java-concurrency/thread-pools.html
https://stackify.com/java-thread-pools/
https://www.geeksforgeeks.org/thread-pools-java/
https://www.javacodegeeks.com/2013/01/java-thread-pool-example-using-executors-and-threadpoolexecutor.html
https://www.journaldev.com/2340/java-scheduler-scheduledexecutorservice-scheduledthreadpoolexecutor-example
https://www.journaldev.com/1069/threadpoolexecutor-java-thread-pool-example-executorservice
http://www.baeldung.com/thread-pool-java-and-guava
https://www.javatpoint.com/java-thread-pool
