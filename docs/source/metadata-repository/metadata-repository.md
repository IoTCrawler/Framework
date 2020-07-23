# MetaData Repository

## What's MetaData Repository

The core component of the architecture of IoTCrawler is what we call MetaData Repository, which can be seen as a Context Broker with the features of distributing information following both query-response and publication-subscription patters among the other components of the IoTCrawler architecture. This Context Broker must be capable of representing semantic, linked data and property graphs. These features have been included in NGSI-LD, a new standard which has been conducted under the ETSI ISG CIM initiative. For this reason, we have selected this technology for the instantiation of our MetaData Repository.

## Choosing MetaData Repository

There are available differents implementations of NGSI-LD context brokers like [Scorpio](https://github.com/ScorpioBroker/ScorpioBroker), [Orion-LD](https://github.com/Fiware/context.Orion-LD) and [Djane](https://github.com/sensinov/djane/). In IoTCrawler architecture, Scorpio is the choosen context broker.

Scorpio is an NGSI-LD compliant context broker developed by NEC Laboratories Europe and NEC Technologies India. This project is part of FIWARE. For more information check the [FIWARE](https://www.fiware.org/) Catalogue entry for [Core Context](https://github.com/Fiware/catalogue/tree/master/core). 

We have selected this context broker for the instantiation of our MetaData Repository because of their features related to the representation of distribution and federation scenarios. Another factor to choosing this broker is the semantic treatment of the information which is more advanced than the rest.

## API - Scorpio

Resources can be managed through the API (e.g. entities and subscriptions). Some of MetaData Repository requests are defined in the next [REST API](metadata-repository-api).

For a detail explaination about the API, please look the ETSI spec.

## How to deploy/test - Scorpio

This component can be deployed following the [README.md](https://github.com/IoTCrawler/ScorpioBroker) file.

Once MetaData Repository is running you can test it. You can find postman collection with sample requests in https://github.com/IoTCrawler/iotcrawler-samples/tree/master/authorization-enabler, you only need to define:

- `MDR-IP`:`MDR-Port` : Endpoint of MDR (Scorpio).