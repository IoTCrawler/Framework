IoTCrawler Model
================
- list out key design features of IoTCrawler e.g.

  * :ref:`MetaData Repository` --- 2 lines description
  * :ref:`Indexing` --- 2 lines description
  * :ref:`Ranking` --- 2 lines description
  * :ref:`Orchestrator` --- 2 lines description
  * :ref:`Search Enabler` --- 2 lines description
  * :ref:`Authorization Enabler` --- 2 lines description
  * :ref:`Semantic Enrichment` --- 2 lines description

.. _MetaData Repository:

MetaData Repository
-------------------
The core component of the architecture of IoTCrawler is what we call MetaData Repository, which can be seen as a Context Broker with the features of 
of distributing information following both query-response and publication-subscription patters among the other components of the IoTCrawler 
architecture. This Context Broker must be capable of representing semantic, linked data and property graphs. These features has been included 
in NGSI-LD, a new standard which has been conducted under the ETSI ISG CIM initiative. For this reason, we have selected this technology for 
the instantiation of our MetaData Repository. 

Scorpio is an NGSI-LD compliant context broker developed by NEC Laboratories Europe and NEC Technologies India. This project is part of 
[FIWARE](https://www.fiware.org/). For more information check the FIWARE Catalogue entry for 
[Core Context](https://github.com/Fiware/catalogue/tree/master/core). We have selected this broker for the instantiation of our MetaData 
Repository because of their features related to the representation of distribution and federation scenarios.

.. _Indexing:

Indexing
--------
The Indexing component  provides a means for clients to search for IoT entities efficiently. It focuses on IoT streams and sensors, where queries 
can be based on sensor type and absolute or relative location. To initiate the process of indexing, a platform manager needs to register a metadata 
broker (MDR) with the Indexing component. In turn this will trigger the subscription to sensors and streams at the registered MDR. As metadata 
descriptions are updated at the MDR, the Indexing component will be notified, and will then index the sensors and streams based on location. 
For scalability, the Indexing component can be configured so that the persistence it relies on (MongoDB) can be sharded. With respect to other 
components in the framework, the Ranking component relies on Indexing for generating the ranking of search results.

.. _Ranking:

Ranking
-------
The Ranking component facilitates ranking mechanism for IoT resources. Ranking and resource selection rely on the registry built (and constantly 
updated) by crawling and indexing methods. The purpose of Ranking is to aid users and applications to not only find a set of resources relevant to 
their needs, but also to select the best or most appropriate one(s) from that set. There are multiple criteria for ranking IoT resources such as
data type, proximity, latency, availability. The Ranking component supports application-dependent,multi-criteria ranking.

.. _Orchestrator:

Orchestrator
------------
The orchestrator component is responsible for interactions with client IoT applications. It allows applications to subscribe to streams without 
having a public endpoint as well as tracks subscription requests. In case of stream failure, orchestrator is able to notify application and provide
a list of alternative streams for subscription.

.. _Search Enabler:

Search Enabler
--------------
The GraphQL-based search enabler component is considered as a main search-component of IoTCrawler. It employs a query language (GraphQL) and a 
query processor, which works on top of NGSI-LD-compliant component (the ranking Component or MDR). The  component eliminates the lack of 
expressivity and functional capabilities which prevent NGSI-LD from being the main search interface the large-scale IoT metadata deployments 
gathered in the IoTCrawler platform. The search enabler fills the gap between low-level sensors and high-level domain semantics about sensors 
data and deals with the context-dependent entities by maintaining the context in the IoTCrawler platform. 

.. _Authorization Enabler:

Authorization Enabler
---------------------
The purpose of this enabler is twofold: on the one hand for a secure communication between the IoTCrawler components, and on the other, for 
controlling the access of the registered users to the resources stored in the IoTCrawler platform. It instantiates the Distributed Capability-Based
Access Control (DCapBAC) technology by using both an XACML framework, and a Capability Manager. This latter is responsible for issuing 
authorizations tokens which must be present in each of the requests aimed at the MetaData Repository.

.. _Semantic Enrichment:

Semantic Enrichment
-------------------
The Semantic Enrichment (SE) component is responsible for annotating data streams with Quality of Information (QoI). To calculate the QoI the 
SE subscribes to the MDR for changes in IoTStreams. When receiving notifications for a stream it takes the related metadata of the stream and 
generates the QoI annotation, which is stored in the MDR afterwards to be accessible by other components of the framework.