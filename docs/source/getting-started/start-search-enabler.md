# Start Search-Enabler

Search enabler works on top of NGSI-LD compatible component: 
[Orchestrator](:doc:`start-orchestrator`), [Ranking Component](:doc:`start-ranking-component`) or [Metadata Repository](:doc:`start-metadata-repository`)
Make sure that at least one of these two component is already running.

Configuration of search-enabler is stored in [docker-compose](https://github.com/IoTCrawler/Search-Enabler/blob/master/docker-compose.yml) file. Clone the [repository](https://github.com/IoTCrawler/Search-Enabler) to have the file locally:

```
git clone https://github.com/IoTCrawler/Search-Enabler
cd search-enabler
```
Please make sure that you've checked/adjusted environment variables according to [documentation](https://github.com/IoTCrawler/Search-Enabler). Execute the following command to run search-enabler:

```
docker-compose up -f docker-compose.yml
```

Output of a successfull start expected to be similar to following:

```
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/app/libs/logback-classic-1.2.3.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/app/libs/slf4j-log4j12-1.7.15.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [ch.qos.logback.classic.util.ContextSelectorStaticBinder]

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.1.6.RELEASE)

INFO 1 --- [           main] c.a.i.graphqlEnabler.HttpApplication     : Starting HttpApplication on e8fdbea680b9 with PID 1 (/app/classes started by root in /)
INFO 1 --- [           main] c.a.i.graphqlEnabler.HttpApplication     : No active profile set, falling back to default profiles: default
INFO 1 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
INFO 1 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
INFO 1 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.21]
INFO 1 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
INFO 1 --- [           main] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 5160 ms
INFO 1 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
INFO 1 --- [           main] o.s.b.a.w.s.WelcomePageHandlerMapping    : Adding welcome page: class path resource [static/index.html]
INFO 1 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
INFO 1 --- [           main] c.a.i.graphqlEnabler.HttpApplication     : Started HttpApplication in 9.806 seconds (JVM running for 11.245)
```

You can check the running containers with following command.

```
docker ps -a
```
The command should return you the following output:
```
gitlab.iotcrawler.net:4567/search-enabler/search-enabler/master   "java -server -cp /a…"   15 hours ago        Up 1 hours         0.0.0.0:8080->8080/tcp  search-enabler_search-enabler_1_4d46b42a3691
```

If everything is running fine then you should be able to see GraphiQL environment by opening the URL `http://localhost:8080` in any web browser.


You can stop the containers and clean your environment when you are finished.

```
docker-compose -f docker-compose.yml down
```
