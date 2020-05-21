# IoTCrawler Framework
IoTCrawler is a research project funded under the European Union's Horizon 2020 reserach and innovation program. The aim of the project is to develop a search engine for the Internet of Things (IoT), enabling search on it’s devices. IoTCrawler focuses on integration and interoperability across different platforms, dynamic and reconfigurable solutions for discovery and integration of data and services from legacy and new systems, adaptive, privacy-aware and secure algorithms and mechanisms for crawling, indexing, and search in distributed IoT systems. The project spans industry, universities and cities. It is comporised of multiple components:
## [Scorpio Broker](https://github.com/IoTCrawler/ScorpioBroker)
Scorpio is an NGSI-LD compliant context broker. 
## [Indexing](https://github.com/IoTCrawler/Indexing)
As a core component in the IoTCrawler framework, Indexing provides a means for clients to search for IoT entities efficiently. It focuses on IoT streams and sensors, where queries can be based on sensor type and absolute or relative location. To initiate the process of indexing, a platform manager needs to register a metadata broker (MDR) with the Indexing component. In turn this will trigger the subscription to sensors and streams at the registered MDR. As metadata descriptions are updated at the MDR, the Indexing component will be notified, and will then index the sensors and streams based on location. For scalability, the Indexing component can be configured so that the persistence it relies on (MongoDB) can be sharded. With respect to other components in the framework, the Ranking component relies on Indexing for generating the ranking of search results.
## [Ranking](https://github.com/IoTCrawler/Ranking)
The Ranking component facilitates ranking mechanism for IoT resources. Ranking and resource selection rely on the registry built (and constantly updated) by crawling and indexing methods. The purpose of Ranking is to aid users and applications to not only find a set of resources relevant to their needs, but also to select the best or most appropriate one(s) from that set. There are multiple criterias for ranking IoT resources such as data type, proximity, latency, availability. The Ranking component supports application-dependent,multi-criteria ranking.
## [Orchestrator](https://github.com/IoTCrawler/Orchestrator)

## [Keyrock](https://github.com/IoTCrawler/Keyrock)
Keyrock is the FIWARE component responsible for Identity Management. Using Keyrock (in conjunction with other security components such as PEP Proxy and Authzforce) enables you to add OAuth2-based authentication and authorization security to your services and applications.
## [Search Enabler](https://github.com/IoTCrawler/Search-Enabler)
## Authorization Enabler
### [XACML PAP PDP](https://github.com/IoTCrawler/XACML_PAP_PDP)
### [Capability Manager](https://github.com/IoTCrawler/Capability-Manager)
### [Security Facade](https://github.com/IoTCrawler/Security-Facade)
## [Pattern Extractor](https://github.com/IoTCrawler/Pattern-Extractor)
## [Semantic Enrichment](https://github.com/IoTCrawler/SemanticEnrichment)
