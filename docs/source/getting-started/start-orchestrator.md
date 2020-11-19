# Start Orchestrator

Orchestrator works on top of [Metadata Repository](start-metadata-repository.html) (handles subscription requests) or the [Ranking Component](start-ranking-component.html)(handles all types of GET requests).
Make sure that at least one of these two component is already running.

Configuration of orchestrator and supplementary services is described in the [docker-compose](https://github.com/IoTCrawler/Orchestrator/blob/master/com.agtinternational.iotcrawler.orchestrator/docker-compose.yml) file. Clone the [repository](https://github.com/IoTCrawler/Orchestrator) to have the file locally:

```
git clone https://github.com/IoTCrawler/Orchestrator
cd orchestrator
cd com.agtinternational.iotcrawler.orchestrator
```

Make sure that you've checked/adjusted environment variables according to the [Documentation](../orchestrator/orchestrator.html). To run orchestrator and other services execute the following command:

```
docker-compose up -f docker-compose.yml
```

This will start the docker containers for Orchestrator and RabbitMQ. Output of the command will be similar to following.

```
INFO [com.agtinternational.iotcrawler.orchestrator.Orchestrator] - <Initializing web server>
DEBUG [com.agtinternational.iotcrawler.orchestrator.clients.NgsiLD_MdrClient] - <Initializing NgsiLD_MdrClient to http://155.54.95.248:9090/ngsi-ld/. CurURIs=false>
INFO [com.agtinternational.iotcrawler.fiware.clients.NgsiLDClient] - <This product includes software developed by NEC Europe Ltd>
INFO [com.agtinternational.iotcrawler.orchestrator.Orchestrator] - <Initialized NGSI-LD Client to http://155.54.95.248:9090>
INFO [com.agtinternational.iotcrawler.orchestrator.Orchestrator] - <Starting orchestrator>
INFO [com.agtinternational.iotcrawler.orchestrator.Orchestrator] - <Syncing with Redis at redis://redis>
INFO [com.agtinternational.iotcrawler.orchestrator.Orchestrator] - <Initializing web server>
DEBUG [com.agtinternational.iotcrawler.core.clients.RabbitClient] - <Trying connect to Rabbit at rabbit>
INFO [com.agtinternational.iotcrawler.orchestrator.HttpServer] - <Trying to init web server for listening at 0.0.0.0:3001>
INFO [com.agtinternational.iotcrawler.orchestrator.HttpServer] - <Adding endpoint http://0.0.0.0:3001/notify>
INFO [com.agtinternational.iotcrawler.orchestrator.HttpServer] - <Adding endpoint http://0.0.0.0:3001/ngsi-ld>
INFO [com.agtinternational.iotcrawler.orchestrator.HttpServer] - <Adding endpoint http://0.0.0.0:3001/>
INFO [com.agtinternational.iotcrawler.orchestrator.Orchestrator] - <Starting built-in web server>
DEBUG [com.agtinternational.iotcrawler.core.clients.RabbitClient] - <Connection to Rabbit rabbit established>
```

You can check the running containers with following command:

```
docker ps -a
```
The command should return you the following output:
```
d6843fcca0ae        gitlab.iotcrawler.net:4567/orchestrator/orchestrator/master   "java -server -cp /a…"   
af9c84616883        rabbitmq:management                                           "docker-entrypoint.s…"  
```

If everything is running fine then you should be able to see the version by executing the following command:

```
curl http://localhost:3001/version
```

You can stop the containers and clean your environment when you are finished.

```
docker-compose -f docker-compose.yml down
```
