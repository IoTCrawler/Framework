# Start MetaData Repository

Download the [Docker Compose](https://github.com/IoTCrawler/iotcrawler-samples/blob/master/getting-started/mdr/docker-compose-mdr.yml) file, go to the directory and run following command.

```
docker-compose up -f docker-compose-mdr.yml -d
```

This will start the docker containers for kafka, postgres, zookeeper and scorpio broker. Output of the command will be similar to following.

```
Creating network "mdr_default" with the default driver
Creating mdr_zookeeper_1 ... done
Creating mdr_postgres_1  ... done
Creating mdr_kafka_1     ... done
Creating mdr_scorpio_1   ... done

```

You can check the running containers with following command.

```
docker ps -a
```

If everything is running fine then you are ready to add your first entity. Use the following command.

```
curl -X POST 'http://localhost:9090/ngsi-ld/v1/entities/' --header 'Content-Type: application/ld+json' -d '{
  "id": "house1:smartrooms:room1",
  "type": "Room",
  "temperature": {
        "value": 21,
        "unitCode": "CEL",
        "type": "Property",
        "providedBy": {
                "type": "Relationship",
                "object": "smartbuilding:house1:sensor001"
         }
   },
  "isPartOf": {
        "type": "Relationship",
        "object": "smartcity:houses:house1"
  },
  "@context": [{"Room": "urn:mytypes:room", "temperature": "myuniqueuri:temperature", "isPartOf": "myuniqueuri:isPartOf"},"https://uri.etsi.org/ngsi-ld/v1/ngsi-ld-core-context.jsonld"]
}'
```

You can get the entity back with following request.

```
curl http://localhost:9090/ngsi-ld/v1/entities/house1:smartrooms:room1
```

You can remove the containers and clean your environment when you are finished.

```
docker-compose -f docker-compose-mdr.yml down
```
