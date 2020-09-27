# Introduction

As part of the Semantic Enrichment component, the Pattern Extraction (PE) module enables the generation of higher-level context by analysing the annotated IoT data streams retrieved from IoT data sources that are pushed to the Metadata Repository (MDR). The Pattern Extractor uses the ```iot-stream:StreamObservations``` to detect higher-level events, which are then published to the broker. A machine learning method is used to analyse a group of ```sosa:observesProperties```. This analysis model is registered as a new subscription in the broker. This subscription includes spatial and temporal and the data type specifications for data streams. Once a stream matches the specifications of a registered process, the pattern extractor then caches the observations that are necessary to perform the analysis. When the observations are received for each stream in the group, the pattern extractor constructs a time window to analyse the data. The result of the analysis is a label for a pattern of data. This label, together with the start and end times of the pattern, is then represented as an ‘’’iot-stream:Event’’’ NGSI-LD entity and published into the broker. The broker then makes these patterns searchable.

## Known dependencies  
  
- MDR  

## Deployable Container  

- Docker  

## Installation  

The Pattern Extraction is provided with an `*.env` file for setting environmental variables, a Dockerfile and Docker-Compose file. The first step is to configure the environment variables in the `*.env` file, which relate to:  
  
- Persistence address and credentials
- Authentication enablement, addresses and credentials.
- Broker address and API operation restriction
- TLS validation enablement  

A template file `env.example` is provided which should be used and saved as an `.*env` file. Once these variables are set, the local persistence used, in this case MongoDB, needs to be configured and running in order for the pattern extraction to run. A mongoDB script needs to be run on the target Mongo instance, which will create an admin user and also a database with a user. The script must be edited to mirror the persistence address and credentials set in the `env` file.
  
For deployment, this can be done by either compiling the project source using npm, or by using docker-compose, which will use the Dockerfile to instantiate the pattern extraction module in a container, in addition to creating containers for the required MongoDB instances. The steps to achieve this are by using the commands below in a terminal:  

1. Build docker images  
```docker-compose build```

2. Create docker containers  
```docker-compose up --no-start```  

3. Start Mongo DB  
```docker-compose start mongo```  

4. Login into mongo container and configure authentication (execute command from mongodb/scripts/mongo.js in the mongo shell).  
```docker exec -it pattern-mongo mongo```  

5. Start Pattern Extractor service  
```docker-compose start patternExtractor```  

This will start a docker container called “patternExtractor”.
  