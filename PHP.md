https://pulsar.incubator.apache.org/docs/latest/applications/JavaClient/
https://next.smashingmagazine.com/2017/04/guide-http2-server-push/
https://www.bitcoinmining.com/getting-started/



https://github.com/mraible/microservices-for-the-masses/blob/master/demos/jhipster-microservices/TUTORIAL.md
https://www.sitepoint.com/build-lyrics-website-laravel-scout-algolia/
http://www.rabbitmq.com/configure.html#config-location
https://github.com/mraible/microservices-for-the-masses/blob/master/demos/jhipster-microservices/TUTORIAL.md
stackdriver
https://www.pgs-soft.com/big-data-and-machine-learning-with-apache-spark-and-cassandra-part-1-architecture/
https://www.infoq.com/articles/traffic-data-monitoring-iot-kafka-and-spark-streaming
http://rancher.com/swarm/
https://www.openstack.org/
http://oskarhane.com/backup-mysql-with-git/
https://www.digitalocean.com/community/tutorials/how-to-configure-sensu-monitoring-rabbitmq-and-redis-on-ubuntu-14-04
https://tech.rgou.net/en/linux-2/backup-script-on-google-drive-for-linux/
http://sivareddy.in/automatic-backup-project-data-git
http://winterbe.com/posts/2014/07/31/java8-stream-tutorial-examples/
(function () {
    'use strict';

    angular
        .module('innovationApp')
        .controller('HomeController', HomeController);

    HomeController.$inject = ['$scope', 'Principal', 'LoginService',
     '$state', 'ECHARTS_THEME1', 'ECHARTS_THEME2', 'ECHARTS_THEME3', '$http','toastr', '$rootScope', '$interval', 'ScreenService'];

    function HomeController($scope, Principal, LoginService,
     $state, ECHARTS_THEME1, ECHARTS_THEME2, ECHARTS_THEME3, $http, toastr, $rootScope, $interval, ScreenService) {
        var client = new ClientJS();
        var vm = this;
        var rightTextStackChart  = '15%';
        vm.heightOveralStatistic = '650px';
        vm.heightStackedChart    = '283px';
        vm.grleft                = '7%';
        vm.legendRight           = "0%";
        vm.bottomStackbar        = '25%';
        if (ScreenService.isHD()){
            console.log("HD");
            var rightTextStackChart = '20%';
            vm.heightOveralStatistic = '455px';
            vm.heightStackedChart = '186px';
            vm.grleft = '5%';
            vm.bottomStackbar = '15%';
            vm.legendRight ="0%";
        }
        vm.account = null;
        vm.isAuthenticated = null;
        vm.login = LoginService.open;
        vm.register = register;
        vm.selectedTeam = "";

        vm.dashboardStatistic = {
            total: 0,
            meetTarget: 0,
            missedTarget: 0,
            warning: 0,
            processing: 0,
            delay: 0,
            completed: 0,
            dropped: 0
        };

        $rootScope.$on('authenticationSuccess', function () {
            getAccount();
        });

        getAccount();

        function getAccount() {
            Principal.identity().then(function (account) {
                vm.account = account;
                vm.isAuthenticated = Principal.isAuthenticated;
            });
        }
        function register() {
            $state.go('register');
        }

        var theme1 = ECHARTS_THEME1();
        var theme2 = ECHARTS_THEME2();
        var theme3 = ECHARTS_THEME3();
        var cavasEchartDonut = document.getElementById('echart_donut');
        cavasEchartDonut.style.height = vm.heightOveralStatistic;
        var echartDonut = echarts.init(cavasEchartDonut, theme1);
        var echartDonutOptions = {
            tooltip: {
                trigger: 'item',
                formatter: "{b} : {c} ({d}%)"
            },
            calculable: true,
            toolbox: {
                show: true,
                feature: {
                    saveAsImage: { title: 'Save image' }
                },
                right: 20,
                top: 30
            },
            series: [
                {
                    name: 'SEV',
                    type: 'pie',
                    radius: [0, '20%'],
                    label: {
                        normal: {
                            show: true,
                            position: 'center',
                            textStyle: {
                                color: '#4631a0',
                                fontSize: '60',
                                fontWeight: 'bold'
                            }
                        }
                    },
                    data: [
                        { value: 1450, name: 'SEV' }
                    ]
                }, {
                    name: 'Team',
                    selectedMode: 'single',
                    type: 'pie',
                    radius: ['40%', '80%'],
                    avoidLabelOverlap: false,
                    label: {
                        normal: {
                            show: true,
                            position: 'inside',
                            formatter: '{d}%'
                        }
                    },
                    data: [{
                        value: 335,
                        name: 'A'
                    }, {
                        value: 310,
                        name: 'B'
                    }]
                }]
        }
        var canvasStackTargetChart = document.getElementById('echart_stack_target');
        canvasStackTargetChart.style.height = vm.heightStackedChart;
        var echartStackTarget = echarts.init(canvasStackTargetChart, theme3);
         
        var echartsStackTargetOption = {
            tooltip: {
                trigger: 'axis',
                axisPointer: {
                    type: 'shadow'
                },
            },
            legend: {
                orient: 'vertical',
                // x: 'right',
                y: 'center',
                align: 'left',
                right: vm.legendRight,
                itemGap: 20,
                data: ['Meet Target', 'Missed Target', 'Warning']
            },
            toolbox: {
                show: true,
                feature: {
                    saveAsImage: { title: 'Save image' }
                },
                right: 20
            },
            dataZoom: [{
                type: 'inside',
                start: 0,
                end: 100
            }],
            grid: {
                left: vm.grleft,
                bottom: vm.bottomStackbar,
                right: rightTextStackChart,
                height: '75%',
                containLabel: true
            },
            xAxis: [
                {
                    type: 'category',
                    axisTick: {
                        show: true
                    },
                    axisLabel: {
                        interval: 0,
                        rotate: 30,
                        textStyle: {
                            color: "#000"
                        }
                    },
                    data: [
                }
            ],
            yAxis: [
                {
                    type: 'value'
                }
            ],
            series: [
                {
                    name: 'Warning',
                    type: 'bar',
                    stack: 'stack',
                    data: [4, 6, 1, 2, 10, 4, 8, 3, 1, 1, 7, 0, 0, 3, 2, 1]
                },
                {
                    name: 'Missed Target',
                    type: 'bar',
                    stack: 'stack',
                    data: [2, 3, 0, 1, 2, 7, 1, 2, 0, 1, 1, 0, 2, 0, 2, 0]
                },
                {
                    name: 'Meet Target',
                    type: 'bar',
                    stack: 'stack',
                    data: [1, 3, 0, 2, 3, 3, 0, 2, 2, 2, 1, 2, 0, 1, 0, 0]
                }
            ]
        };
        var canvasStackStatus = document.getElementById('echart_stack_status');
        canvasStackStatus.style.height = vm.heightStackedChart;
        var echartStackStatus = echarts.init(canvasStackStatus, theme2);
        var echartStackStatusOption = {
            tooltip: {
                trigger: 'axis',
                axisPointer: {
                    type: 'shadow'
                }
            },
            legend: {
                orient: 'vertical',
                // x: 'right',
                y: 'center',
                align: 'left',
                right: vm.legendRight,
                itemGap: 20,
                // data: ['Processing', 'Delay', 'Completed', 'Dropped']
                data: ['On Time', 'Delay']
            },
            toolbox: {
                show: true,
                feature: {
                    saveAsImage: { title: 'Save image' }
                },
                right: 20,
            },
            dataZoom: [{
                type: 'inside',
                start: 0,
                end: 100
            }],
            grid: {
                left: vm.grleft,
                bottom: vm.bottomStackbar,
                right: rightTextStackChart,
                height: '75%',
                containLabel: true
            },
            xAxis: [
                {
                    type: 'category',
                    boundaryGap: true,
                    axisTick: { onGap: false },
                    splitLine: { show: false },
                    axisLabel: {
                        interval: 0,
                        rotate: 30,
                        textStyle: {
                            color: "#000"
                        }
                    },
                    data: ['A', 'B', 'C']
                }
            ],
            yAxis: [
                {
                    type: 'value'
                }
            ],
            series: [
                // {
                //     name: 'Dropped',
                //     type: 'bar',
                //     stack: 'stack',
                //     data: [1, 3, 0, 2, 3, 3, 0, 2, 2, 2, 1, 2, 0, 1, 0, 0]
                // },
                // {
                //     name: 'Completed',
                //     type: 'bar',
                //     stack: 'stack',
                //     data: [2, 3, 0, 1, 2, 7, 1, 2, 0, 1, 1, 0, 2, 0, 2, 0]
                // },
                {
                    name: 'Delay',
                    type: 'bar',
                    stack: 'stack',
                    data: [4, 6, 1, 2, 10, 4, 8, 3, 1, 1, 7, 0, 0, 3, 2, 1]
                },
                // {
                //     name: 'Processing',
                //     type: 'bar',
                //     stack: 'stack',
                //     data: [4, 6, 1, 2, 10, 4, 8, 3, 1, 1, 7, 0, 0, 3, 2, 1]
                // },
                {
                    name: 'On Time',
                    type: 'bar',
                    stack: 'stack',
                    data: [4, 6, 1, 2, 10, 4, 8, 3, 1, 1, 7, 0, 0, 3, 2, 1]
                }

            ]
        };

        function drawChartDetail(team) {
            $http.get("/api/projects/detail-project-by-team", { params: { team: team != null ? team : "" } })
                .then(function (response) {
                    if (response.data instanceof Object) {
                        echartsStackTargetOption.xAxis[0].data = response.data.item;
                        echartsStackTargetOption.series[0].data = response.data.warning;
                        echartsStackTargetOption.series[1].data = response.data.missedTarget;
                        echartsStackTargetOption.series[2].data = response.data.meetTarget;
                        echartStackTarget.setOption(echartsStackTargetOption);

                        echartStackStatusOption.xAxis[0].data = response.data.item;
                        // echartStackStatusOption.series[0].data = response.data.dropped;
                        // echartStackStatusOption.series[1].data = response.data.completed;
                        echartStackStatusOption.series[0].data = response.data.delay;
                        // echartStackStatusOption.series[3].data = response.data.processing;
                        echartStackStatusOption.series[1].data = response.data.processing;
                        echartStackStatus.setOption(echartStackStatusOption);

                        vm.dashboardStatistic.warning = 0;
                        angular.forEach(response.data.warning, function (v) {
                            vm.dashboardStatistic.warning += v;
                        });

                        vm.dashboardStatistic.missedTarget = 0;
                        angular.forEach(response.data.missedTarget, function (v) {
                            vm.dashboardStatistic.missedTarget += v;
                        });

                        vm.dashboardStatistic.meetTarget = 0;
                        angular.forEach(response.data.meetTarget, function (v) {
                            vm.dashboardStatistic.meetTarget += v;
                        });

                        vm.dashboardStatistic.dropped = 0;
                        angular.forEach(response.data.dropped, function (v) {
                            vm.dashboardStatistic.dropped += v;
                        });

                        vm.dashboardStatistic.completed = 0;
                        angular.forEach(response.data.completed, function (v) {
                            vm.dashboardStatistic.completed += v;
                        });

                        vm.dashboardStatistic.delay = 0;
                        angular.forEach(response.data.delay, function (v) {
                            vm.dashboardStatistic.delay += v;
                        });

                        vm.dashboardStatistic.processing = 0;
                        angular.forEach(response.data.processing, function (v) {
                            vm.dashboardStatistic.processing += v;
                        });

                    }
                }, function (response) {
                    console.log(response);
                });
        }
        function loadDataChart() {
            console.log("Reload data chart");
            $http.get("")
                .then(function (response) {
                    if (response.data instanceof Array) {
                        var total = 0;
                        angular.forEach(response.data, function (item) {
                            total += item.value;
                        });
                        vm.dashboardStatistic.total = total;
                        echartDonutOptions.series[0].data = [{ value: total, name: 'SEV' }];
                        echartDonutOptions.series[1].data = response.data;
                        echartDonut.setOption(echartDonutOptions);

                        drawChartDetail();
                    }
                }, function (response) {
                    console.log(response);
                });
        }
        function autoReloadDataChart(seconds, callback) {
            callback();
            return $interval(callback, seconds * 1000);
        }
        autoReloadDataChart(300, loadDataChart);
        
        echartDonut.on("click", function (param) {
            // console.log(echartDonut);
            // console.log(param);

            var text = $("#selected_team_text");
            if (param.seriesName == 'Team' && param.data.selected == true) {
                vm.selectedTeam = param.name;
                text.html(param.name);
                text.css({ "color": param.color });
                drawChartDetail(vm.selectedTeam);
                vm.dashboardStatistic.total = param.value;
            } else {
                vm.selectedTeam = "TEST";
                text.html("TEST");
                text.css({ "color": "#fff" });
                echartDonut.setOption(echartDonutOptions);
                vm.dashboardStatistic.total = echartDonut._chartsViews[0]._data._rawData[0].value
                drawChartDetail();
            }
        });

    }
})();


# https://www.smashingmagazine.com/2017/06/better-faster-optimized-wordpress-websites/
# https://resin.io/
# https://kndrck.co/indexing-faces-on-instagram.html
# https://www.aiia.net/artificial-intelligence/articles/what-get-the-app-means-for-big-data-and-for/?=37423874
# https://www.startupschool.org/presentations/vertical/artificial-intelligence
# https://research.googleblog.com/2017/06/supercharge-your-computer-vision-models.html
# https://github.com/creativetimofficial/paper-dashboard
# http://eventregistry.org/
# https://github.com/EbookFoundation/free-programming-books/blob/master/free-programming-books.md#spring-boot
# https://bookmarks.codingpedia.org/
# https://www.diffbot.com/products/automatic/article/
# http://tomazkovacic.com/blog/2011/03/11/list-of-resources-article-text-extraction-from-html-documents/
# https://www.ibm.com/watson/developercloud/alchemy-language/api/v1/#authentication
# http://tomazkovacic.com/blog/2011/03/11/list-of-resources-article-text-extraction-from-html-documents/
# https://www.gipp.com/wp-content/papercite-data/pdf/hamborg2017.pdf
# https://www.gipp.com/wp-content/papercite-data/pdf/hamborg2017.pdf
# https://www.quora.com/Web-Crawling-How-can-you-extract-news-articles-given-keywords-and-news-sources
# https://www.mkyong.com/java/jsoup-basic-web-crawler-example/
# http://www.geeksforgeeks.org/performing-google-search-using-python-code/
# http://www.pac4j.org/index.html
# https://www.sitepoint.com/top-javascript-frameworks-libraries-tools-use/
# https://blog.ambar.cloud/ingesting-documents-pdf-word-txt-etc-into-elasticsearch/
# https://medium.mybridge.co/machine-learning-top-10-articles-for-the-past-month-b499e4213a34
# https://uxdesign.cc/design-better-data-tables-4ecc99d23356
# http://urban.nyasha.me/angular/#/
# Webmaster GUide line
https://github.com/openimages/dataset
https://www.drift.com/pricing/
- http://www.techiedelight.com/data-structures-and-algorithms-interview-questions-stl/
- https://support.google.com/webmasters
# 360 
- https://blog.vrtigo.io/do-people-view-all-360-f60b858059fe#.jvic30ufb
# PHP awesome

- https://github.com/linuxkit/linuxkit
- https://github.com/ziadoz/awesome-php
- https://github.com/MaximAbramchuck/awesome-interview-questions
- https://gist.github.com/messified/6381844
- https://github.com/developerquestions/php-questions
- https://github.com/h5bp/Front-end-Developer-Interview-Questions
- https://github.com/uhub/awesome-php
- https://gist.github.com/Brammm/7009248

- CodeIgniter Framework
 + https://www.codeigniter.com/userguide3/general/welcome.html
 + Install GUI https://www.codeigniter.com/userguide3/installation/index.html
 + HMVC (http://www.roytuts.com/setup-hmvc-with-codeigniter-3/)
 + htaccess (https://github.com/wolfgang1983/htaccess_for_codeigniter)
 + https://www.codeigniter.com/userguide3/general/routing.html
 
- Composer
- HVMC
- Backfire.io
- LAMP
- LEMP
- http://overapi.com/php
- https://code.tutsplus.com/tutorials/hmvc-an-introduction-and-application--net-11850

# Javascript Awesome

- AngularJs
 + Yeoman Angularjs (https://github.com/yeoman/generator-angular)
 + http://cgross.github.io/angular-busy/demo/
 + https://www.bennadel.com/blog/2758-creating-a-pre-bootstrap-loading-screen-in-angularjs.htm
 + http://revillweb.github.io/angular-preload-image/
 + https://www.bennadel.com/blog/2597-preloading-images-in-angularjs-with-promises.htm
 + http://www.code-hound.com/add-a-preloader-to-your-website-using-angularjs/
 + http://cgross.github.io/angular-busy/demo/
 + http://waseembepari.github.io/angular-material-preloader/
 + https://sc5.io/posts/how-to-implement-loaders-for-an-angularjs-app/
 + https://blog.sourceclear.com/improving-the-angular-single-page-application-loading-experience/
 + http://pathgather.github.io/please-wait/
 + http://victorbjelkholm.github.io/ngProgress/
 + http://stackoverflow.com/questions/30107459/how-to-do-preloader-for-ng-view-in-angular-js
 + https://chieffancypants.github.io/angular-loading-bar/#
 + https://www.bignerdranch.com/blog/music-visualization-with-d3-js/
 + https://dzone.com/articles/exploring-html5-web-audiohttps://dzone.com/articles/exploring-html5-web-audio
 + https://medium.com/@_2988845157752/how-to-develop-an-im-bot-for-facebook-messenger-b09cb4372538#.ytbxuhhg2
# React

 + https://github.com/mxstbr/react-boilerplate
 + https://github.com/kriasoft/react-starter-kit
 + https://github.com/badsyntax/react-seed
 + https://github.com/feroult/yawp
# NodeJs
 - Yeoman 
 - Grunt
 - Bower
 - Gulp
 
# Development Tools

- Vagrant (https://github.com/fideloper/Vaprobash)
- Capistrano (Deploy tools)
- Docker (Application container)

# Continuous Delivery

- http://codeship.com/
- https://travis-ci.org/
- Jenkins

# Version Control System

- GIT (Git flow, git work flow)
 + Gitignore (https://git-scm.com/docs/gitignore)
 + https://github.com/github/gitignore
- SVN
- P4

# Unbuntu

- Vim (https://vim.rtorr.com/)
- rsync
- http://www.cheat-sheets.org/saved-copy/ubunturef.pdf
- https://www.nixtutor.com/linux/all-the-best-linux-cheat-sheets/

# Webserver

- Apache2
 - mod_rewrite (https://mediatemple.net/community/products/dv/204643270/using-htaccess-rewrite-rules) .httacces
- Nginx

# Bigdata

- http://blog.cloudera.com/blog/2014/09/getting-started-with-big-data-architecture/

# Java 8

- Java 8: New features in ConcurrentHashMap [http://www.deadcoderising.com/2016-01-17-java-8-new-features-in-concurrenthashmap/]

# Javascript

- 2016 JavaScript Rising Stars [https://risingstars2016.js.org/#all]
- Wepack gitbook (http://survivejs.com/webpack/handling-styles/loading/)
- https://github.com/legomushroom/mojs
# Mongo DB

- https://snyk.io/blog/mongodb-hack-and-secure-defaults/

# CSS
- https://yeun.github.io/open-color/

# New DB

- https://www.cockroachlabs.com/

- https://yeun.github.io/open-color/ingredients.html

# Search

- https://moz.com/beginners-guide-to-seo/search-engine-tools-and-services

# Git

- Gitea [https://gitea.io/en-US/]
- http://www.krihelinator.xyz/languages

# IOT

- https://home-assistant.io/components/

# Cloud 

- https://releases.openstack.org/newton/index.html

# Lavarel

- Lavarel Seed Project [http://laravel-boilerplate.com/start.html]

# Software Development
- https://www.linkedin.com/pulse/software-project-team-rolescontinuing-writing-editing-farhana-sharmin

# Seo

- Cost-per-click (CPC) https://support.google.com/adsense/answer/32725?hl=en&ref_topic=1113898
- https://www.woorank.com
	
# WebSEO Tools

 http://www.webseoanalytics.com/
 http://inet.edu.vn/tin-tuc/2984/google-keyword-tool.html
 http://seokool.com/3-cach-kiem-tra-thu-hang-tu-khoa-chinh-xac-nhat-tren-google/
 
- Toi uu hoa keyword 

- https://thietkewebchuanseo.com/kien-thuc-seo_chia-se-kien-thuc/5-cach-tang-thu-hang-tu-khoa-tren-top-google/
 
# Xay dung back link 

- http://neilpatel.com/blog/improve-google-rankings-without-getting-penalized/
- http://www.mtu.edu/umc/services/digital/seo/
- https://majestic.com/account/register
- https://support.google.com/webmasters/answer/47334?hl=en

# Search box

 - https://developers.google.com/search/docs/data-types/sitelinks-searchbox
 
# Architecture

 + Evetn driven
 
  - https://martinfowler.com/articles/201701-event-driven.html
  - https://spring.io/guides/gs/messaging-reactor/
  
# Sercurity

- https://jhalderm.com/pub/papers/interception-ndss17.pdf

# RethinkDB (Realtime DB)

- rethinkdb
- https://geowarin.github.io/spring-boot-and-rethinkdb.html

# HTML & CSS

- https://internetingishard.com/html-and-css/

# Image compare

- http://rembrandtjs.com/

# Microservices

- https://networknt.github.io/light-java/getting-started/
- https://spring.io/blog/2015/07/14/microservices-with-spring
- https://qbox.io/blog/elasticsearch-in-apache-spark-python

# Geeks

- http://www.adeveloperdiary.com/
- http://sitepoint.com
- http://www.mhthemes.com/lite/?theme=tuto
- https://www.sitepoint.com/premium/screencasts/how-to-utilize-data-structures-in-elm-when-building-an-app
- scoth.io
- https://github.com/CloudCannon/edition-jekyll-template
- https://tympanus.net/codrops/
- http://www.tutorialsteacher.com/jquery/jquery-selectors
- docs.io
- http://www.wpbeginner.com/wp-themes/how-to-create-a-custom-page-in-wordpress/
- https://shopify.github.io/liquid/
- https://github.com/terryum/awesome-deep-learning-papers
- https://www.khanacademy.org/computing/computer-science

# Sercurity

- https://docs.securedrop.org/en/latest/admin.html

# Proxy

- http://www.squid-cache.org/

# Spring

- [Batch Writing, and Dynamic vs Parametrized SQL, how well does your database perform] (http://java-persistence-performance.blogspot.com/2013/05/batch-writing-and-dynamic-vs.html)
- http://kyriakos.anastasakis.net/2015/06/12/batch-inserts-with-spring-data-and-mysql/
- http://www.bmchild.com/2015/02/spring-data-custom-batch-save-repository.html
- https://egkatzioura.wordpress.com/2016/04/29/spring-boot-and-database-initialization/

# Incapsula

- incapsula
- https://www.confluent.io/blog/bottled-water-real-time-integration-of-postgresql-and-kafka/

# Linkin

https://www.linkedin.com/pulse/clickbaits-revisited-deep-learning-title-content-features-thakur
https://blog.codecentric.de/en/2017/02/integration-testing-strategies-spring-boot-microservices/

# Machine Learning

- https://github.com/databricks/spark-knowledgebase

- http://zdatainc.com/2014/08/real-time-streaming-apache-spark-streaming/

- https://dzone.com/articles/analytics-with-apache-spark-tutorial-part-2-spark

- https://dzone.com/articles/using-apache-spark-and-mysql-for-data-analysis

- http://rockthecode.io/tech-events/real-time-big-data-analytics-with-apache-solr-and-spark/

- http://www.scoop.it/t/mongodb-bigdata-search-engine

- https://www.reddit.com/r/MachineLearning/comments/5hwqeb/project_all_code_implementations_for_nips_2016/

# Smart image thumb

- http://blog.algorithmia.com/smart-thumbnail-image-cropping/
- http://cloudinary.com/blog/face_detection_based_cropping
- https://github.com/coobird/thumbnailator
- http://opencvlover.blogspot.com/2012/11/face-detection-in-javacv-using-haar.html
- http://commons.apache.org/proper/commons-imaging/sampleusage.html
- https://github.com/thumbor/thumbor (Best)
- http://blog.mapado.com/image-cropping-entropy-face-detection/
- http://cloudinary.com/blog/beyond_face_detection_smart_cropping_in_the_cloud_using_imagga_and_cloudinary
- https://www.microsoft.com/cognitive-services/en-us/computer-vision-api
- http://commons.apache.org/proper/commons-imaging/sampleusage.html
- https://github.com/coobird/thumbnailator
- https://github.com/kebattai/spring-a-gram
- https://github.com/kebattai/spring-boot-samples/tree/master/spring-boot-file-upload-with-ajax
- https://www.infoq.com/articles/Automate-Docker-Cloud-Java-Microservice-Deployment-with-DCHQ
- https://www.smashingmagazine.com/2016/12/front-end-performance-checklist-2017-pdf-pages/

# OAuth 2

- http://websystique.com/spring-security/secure-spring-rest-api-using-oauth2/
- https://github.com/Baeldung/spring-security-oauth/blob/master/spring-security-oauth-ui-password/src/main/resources/application.yml

# Performace Test

- http://www.baeldung.com/rest-api-search-language-spring-data-querydsl
- https://testmysite.withgoogle.com/intl/en-gb/
- https://varvy.com/pagespeed/
- JMetter2
- Selelium

# TL 

- https://www.algolia.com/infra

- https://motherboard.vice.com/en_us/article/how-our-likes-helped-trump-win

- https://www.buzzfeed.com/

- http://introtodeeplearning.com/schedule.html

- https://ongxuanhong.wordpress.com/2015/12/03/git-notes/

- https://ongxuanhong.wordpress.com/2016/10/26/command-line-thuong-dung/

- https://ongxuanhong.wordpress.com/2016/07/06/machine-learning-cho-nguoi-bat-dau/

- http://gridbyexample.com/

- https://huu.la/ai/cssrooster

- http://www.adeveloperdiary.com/
- http://sitepoint.com
- http://www.mhthemes.com/lite/?theme=tuto
- https://www.sitepoint.com/premium/screencasts/how-to-utilize-data-structures-in-elm-when-building-an-app
- scoth.io
- https://github.com/CloudCannon/edition-jekyll-template
- https://tympanus.net/codrops/

- http://www.tutorialsteacher.com/jquery/jquery-selectors
- docs.io
- http://www.wpbeginner.com/wp-themes/how-to-create-a-custom-page-in-wordpress/
- https://shopify.github.io/liquid/
- https://github.com/terryum/awesome-deep-learning-papers
- https://www.khanacademy.org/computing/computer-science
- https://internetingishard.com/html-and-css/

# Deep learninng

- http://colah.github.io/posts/2015-08-Understanding-LSTMs/
- http://colormind.io/blog/
- https://deeplearning4j.org/lstm
- http://www.kdnuggets.com/news/top-stories.html
- http://imagesloaded.desandro.com/#jquery

#  Tools

- Nagios
- Rackspace
- Splunk
- Chef
- http://docs.ansible.com/ansible/playbooks.html

- http://www.squid-cache.org/
- Grafana
- https://graphiteapp.org/
- Rackspace
- https://www.atlassian.com/git/tutorials/comparing-workflows
- https://chocolatey.org/
- kubernetes
- OpenShift (CloudPlatform)
- ProjectAtomic
- Docker

# Docker

- https://github.com/SUSE/Portus
- http://geekyplatypus.com/dockerise-your-php-application-with-nginx-and-php7-fpm/
- https://github.com/fideloper/docker-nginx-php
- https://get.docker.com/
- https://github.com/kasperisager/php-dockerized.git
- https://docs.docker.com/swarm/swarm_at_scale/deploy-app/#extra-credit-deployment-with-docker-compose

# Chat bot programing

- botman.io
- botkit
- Ngrok

# Git rebase 

- https://github.com/sjurba/rebase-editor
- http://data8.org
- http://www.primaryobjects.com/categories/Programming/

# DNS
- xip.io
- ngrok
- www.powerdns.com
- https://scotch.io/tutorials/get-vagrant-up-and-running-in-no-time
- https://gist.github.com/Iristyle/5171999
- https://www.howtogeek.com/138159/how-to-enable-programs-and-custom-scripts-to-run-at-boot/
- https://freemyip.com/whatsnew
- https://mailcatcher.me/
- http://o7planning.org/en/10259/build-a-multiple-module-project-with-maven#a29581
- winsw
# http://www.johnwittenauer.net/how-to-learn-hadoop-for-free/
# https://blog.blendo.co/blendo-data-monthly-the-kafka-effect/
# http://emmaguo.github.io/angular-poller/
#https://www.thoughtworks.com/insights/blog/bff-soundcloud
#http://www.jqueryscript.net/demo/Medium-style-Floating-Text-highlight-Menu-With-jQuery-CSS3/
#http://www.jqueryscript.net/demo/Medium-style-Floating-Text-highlight-Menu-With-jQuery-CSS3/
#https://www.mkyong.com/java/jsoup-basic-web-crawler-example/
#https://www.sitepoint.com/themes/ecommerce/product-category/bowls/


# Deep learning
- http://www.abigailsee.com/2017/04/16/taming-rnns-for-better-summarization.html
- http://www.abigailsee.com/2017/04/16/taming-rnns-for-better-summarization.html
# JFrog
- https://inthecheesefactory.com/blog/how-to-setup-private-maven-repository/en
- https://medyo.github.io/how-to-set-up-a-private-maven-repository-for-free

- https://medium.com/@lhartikk/development-environment-in-spring-boot-with-docker-734ad6c50b34
- Postal
- http://archive4j.di.unimi.it/
- setting
# Crawl

http://stackoverflow.com/questions/40597051/jhipster-dev-profile-reverse-proxy
http://seanoreillyza.github.io/programming/2015/07/13/enforcing-https-in-jhipster.html
https://github.com/kohlschutter/boilerpipe
https://github.com/codelucas/newspaper
https://www.quora.com/Web-Crawling-How-can-you-extract-news-articles-given-keywords-and-news-sources
https://www.quora.com/Web-Crawling-How-can-you-extract-news-articles-given-keywords-and-news-sources
http://tomazkovacic.com/blog/2011/06/09/evaluating-text-extraction-algorithms/
https://www.quora.com/Whats-the-best-method-to-extract-article-text-from-HTML-documents
http://tomazkovacic.com/blog/2011/03/02/extracting-article-text-from-html-documents/
http://tomazkovacic.com/blog/2011/03/02/extracting-article-text-from-html-documents/
https://code.google.com/archive/p/boilerpipe/
https://github.com/fhamborg/news-please
https://www.quora.com/Web-Crawling-How-can-you-extract-news-articles-given-keywords-and-news-sources
http://stormcrawler.net/


http://recursivechaos.com/blog/spring-boot-jpa-mysql/
http://www.bmchild.com/2015/02/spring-data-custom-batch-save-repository.html
https://frightanic.com/software-development/jpa-batch-inserts/
http://stackoverflow.com/questions/40597051/jhipster-dev-profile-reverse-proxy
http://seanoreillyza.github.io/programming/2015/07/13/enforcing-https-in-jhipster.html
https://github.com/kohlschutter/boilerpipe
https://github.com/codelucas/newspaper
https://www.quora.com/Web-Crawling-How-can-you-extract-news-articles-given-keywords-and-news-sources
https://www.quora.com/Web-Crawling-How-can-you-extract-news-articles-given-keywords-and-news-sources
http://tomazkovacic.com/blog/2011/06/09/evaluating-text-extraction-algorithms/
https://www.quora.com/Whats-the-best-method-to-extract-article-text-from-HTML-documents
http://tomazkovacic.com/blog/2011/03/02/extracting-article-text-from-html-documents/
http://tomazkovacic.com/blog/2011/03/02/extracting-article-text-from-html-documents/
https://code.google.com/archive/p/boilerpipe/
https://github.com/fhamborg/news-please
https://www.quora.com/Web-Crawling-How-can-you-extract-news-articles-given-keywords-and-news-sources
http://stormcrawler.net/


http://recursivechaos.com/blog/spring-boot-jpa-mysql/
http://www.bmchild.com/2015/02/spring-data-custom-batch-save-repository.html
https://frightanic.com/software-development/jpa-batch-inserts/
http://imagesloaded.desandro.com/



http://stackoverflow.com/questions/40597051/jhipster-dev-profile-reverse-proxy
http://seanoreillyza.github.io/programming/2015/07/13/enforcing-https-in-jhipster.html
https://github.com/kohlschutter/boilerpipe
https://github.com/codelucas/newspaper
https://www.quora.com/Web-Crawling-How-can-you-extract-news-articles-given-keywords-and-news-sources
https://www.quora.com/Web-Crawling-How-can-you-extract-news-articles-given-keywords-and-news-sources
http://tomazkovacic.com/blog/2011/06/09/evaluating-text-extraction-algorithms/
https://www.quora.com/Whats-the-best-method-to-extract-article-text-from-HTML-documents
http://tomazkovacic.com/blog/2011/03/02/extracting-article-text-from-html-documents/
http://tomazkovacic.com/blog/2011/03/02/extracting-article-text-from-html-documents/
https://code.google.com/archive/p/boilerpipe/
https://github.com/fhamborg/news-please
https://www.quora.com/Web-Crawling-How-can-you-extract-news-articles-given-keywords-and-news-sources
http://stormcrawler.net/


http://recursivechaos.com/blog/spring-boot-jpa-mysql/
http://www.bmchild.com/2015/02/spring-data-custom-batch-save-repository.html
https://frightanic.com/software-development/jpa-batch-inserts/

http://www.pixelstech.net/article/1474790035-Loading-images-progressively-using-Gaussian-blur
http://www.guypo.com/introducing-lqip-low-quality-image-placeholders/
https://jmperezperez.com/medium-image-progressive-loading-placeholder/
https://github.com/callmecavs/layzr.js/#optional-placeholders
https://www.theodo.fr/blog/2016/10/medium-like-image-loading-with-vue-js/
https://www.webforefront.com/performance/webservers_statictier.html
https://www.nginx.com/resources/admin-guide/serving-static-content/
topic and ng
- https://www.savjee.be/2016/06/Deploying-website-to-ftp-or-amazon-s3-with-BitBucket-Pipelines/
- http://www.baeldung.com/tomcat-deploy-war
- D:\BIGQSYS2017\vinasao2017
- https://www.stardary.com/country/vietnam
- https://developers.facebook.com/docs/graph-api/reference/v2.9/page/feed
- https://github.com/ghostnight123/restfb
- https://github.com/roundrop/facebook4j
- Spring socical
- https://examples.javacodegeeks.com/enterprise-java/quartz/spring-quartz-scheduler-example/

- https://docs.spring.io/spring-boot/docs/current/reference/html/deployment-install.html


#!/bin/bash
service=survey
fileRemove="/etc/init.d/survey"
if (( $(ps -ef | grep -v grep | grep $service | wc -l) > 0 ))
then
  echo "$service is running, stop service..!"
  /etc/init.d/$service stop
  echo "Remove service..!"
  if [! -f  fileRemove ]
  then
    rm  fileRemove
  fi
  DEPLOYFILE=$(find target -name '*.war' | xargs echo | tr ' ' ':')
  ln -s /$DEPLOYFILE /etc/init.d/$service
  echo $DEPLOYFILE
  /etc/init.d/$service start
else
  echo "Remove service..!"
  if [ ! -f "/etc/init.d/survey" ]
  then
    rm  /etc/init.d/survey
    echo "Removed"
  fi
  cd target
  DEPLOYFILE=$(find -name '*.war' | xargs echo | tr ' ' ':' | cut -d '/' -f 2)
  echo $DEPLOYFILE
  ln -s /var/www/survey/target/$DEPLOYFILE /etc/init.d/$service
  /etc/init.d/$service start
fi

#!/bin/bash
scp -P 2182 -r target dpi@107.113.53.108:/var/www/survey
https://wit.ai/


          $rootScope.$on('$viewContentLoaded', function(event, viewName, viewContent){
              if (viewName=='leftmenu@'){
                initializeLeftMenu();
                initializePanel();
              }
            });
http://aiplaybook.a16z.com/docs/intro/getting-started
https://osf.io/register/
https://mitpress.mit.edu/sites/default/files/titles/content/9780262514293_Creative_Commons_Edition.pdf
https://chatbotsmagazine.com/contextual-chat-bots-with-tensorflow-4391749d0077
https://github.com/ugik/notebooks
https://chatbotsmagazine.com/cheat-sheet-all-facebook-chatbot-interactions-4b14e4e00178
https://www.sitepoint.com/5-most-popular-frontend-frameworks-compared/
https://blog.remix.com/an-intro-to-integer-programming-for-engineers-simplified-bus-scheduling-bd3d64895e92
https://simplesecurity.sensedeep.com/web-developer-security-checklist-f2e4f43c9c56
https://www.smashingmagazine.com/2017/05/json-api-normalizer-redux/
https://simplesecurity.sensedeep.com/web-developer-security-checklist-f2e4f43c9c56
https://aic-project.github.io/documentation/

https://www.howtoforge.com/tutorial/install-mongodb-on-ubuntu-16.04
https://github.com/PGSSoft/pgs-blog/tree/master/SparkProject
https://www.pgs-soft.com/experience/sts-e-commerce/
FakeJSON Server
https://hubot.github.com/
https://hubot.github.com/
https://unsupervisedmethods.com/my-curated-list-of-ai-and-machine-learning-resources-from-around-the-web-9a97823b8524
