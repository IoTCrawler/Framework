Indexing
========

As a core component in the IoTCrawler framework, Indexing provides a
means for clients to search for IoT entities efficiently. It focuses on
IoT streams and sensors, where queries can be based on sensor type and
absolute or relative location. To initiate the process of indexing, a
platform manager needs to register a metadata broker (MDR) with the
Indexing component. In turn this will trigger the subscription to
sensors and streams at the registered MDR. As metadata descriptions are
updated at the MDR, the Indexing component will be notified, and will
then index the sensors and streams based on location. For scalability,
the Indexing component can be configured so that the persistence it
relies on (MongoDB) can be sharded. With respect to other components in
the framework, the Ranking component relies on Indexing for generating
the ranking of search results.

-  `Indexing <#indexing>`__
-  `Indexing and the IoT Crawler
   Architecture <#indexing-and-the-iot-crawler-architecture>`__
-  `Indexing Mechanism <#indexing-mechanism>`__
-  `Query Interface <#query-interface>`__
-  `Implementation <#implementation>`__
-  `Deployment <#deployment>`__

   -  `Initial Setup <#initial-setup>`__
   -  `Run Web Service from Source <#run-web-service-from-source>`__
   -  `Running in Production mode <#running-in-production-mode>`__

Indexing and the IoT Crawler Architecture
-----------------------------------------

In the IoTCrawler architecture, the Indexing component operates within
the processing layer. It interacts primarily with the MDR (Scorpio
Broker) and the Ranking component. Indexing mechanisms are used in order
to support efficient search methods. While MDRs hold the complete
metadata description of a resource, indexes on the other hand, contain
only a subset of the resources’ descriptions. In the case of the Ranking
component, it relies on the efficient search mechanism of the Indexing
component to be able to rank entities based on the search criteria.

Indexing Mechanism
------------------

IoTCrawler supports three types of indexing strategies: spatial,
temporal and thematic.

The index consists of three parts: two indices that map Entity IDs of
IoTStream and sosa:Sensor to geo-partition key, and a geo-partitioned
index containing the data. A partition key is computed according to the
location of the data. The partition key is computed by intersecting
sensor location GeoJSON objects with predefined region GeoJSON polygons.
Entities in the index are stored as a graph. Instead of storing all
entities separately, linked entities are stored as a single document.
The top-level entity is the IoTStream and all related entities are
stored as nested documents in the properties of the parent document.
This structure allows to define compound indices, thus accelerates
nested queries.

Query Interface
---------------

The indexing component includes an NGSI-LD query interface and uses the
data from the broker to respond to common queries. This component
creates a subscription for metadata changes in the broker to keep the
indexes up-to-date. Each time the metadata changes, the indexing
component receives a notification and updates the index appropriately.

It exposes full NGSI-LD querying interface. ``Link`` header or *Temporal
Entities* are **NOT** supported. If query is too complex (contains
RegExp), involes entities (or related entities) or properties which are
not part of the index, it will be forwared to NGSI-LD broker.

Implementation
--------------

Indexing is a Node.js web service written in TypeScript. It uses sharded
MongoDB to store its data. It subscribes to the MDR broker for Stream,
Sensor, QoI and Location changes and uses these notifications to keep
index up-to-date.

Deployment
----------

To deploy the Indexing component, several approaches can be taken.

-  Build and run from source
-  Build and run from Docker container
-  Deploy on Kubernetes Cluster

Initial Setup
~~~~~~~~~~~~~

1. Install dependencies

   As a Node.js project, the dependencies need to first be installed in
   the target machine. In a terminal, the command for this is:

``bash npm install``

2. Configuration of Persistence (MongoDB)

   Indexing makes use of the MongoDB Sharding feaure. This allows the
   distribution of documents among multiple instances of MongoDB
   servers. The minimum number of instances required to enable sharding
   is 4; one acting as the query router, another as a configuration
   server for the sharded cluster, and the other as shards, where each
   contains a subset of the documents stored.

   .. figure:: https://docs.mongodb.com/manual/_images/sharded-cluster-production-architecture.bakedsvg.svg
      :alt: mongo\_sharded

      mongo\_sharded
   To enable this, a set of scripts need to be run. These scripts
   require credentials to be set for the shared cluster and its
   handlers. These can be found under the source folder
   ``mongodb\scripts``. MongoDB setup instructions are located in the ``DEPLOYMENT.md`` guide in the source repository.
   

3. Environment Variables

The web service reads environment variables to be able to configure
itself relation to details for persistence, security endpoints, and
default brokers. To do this, an ``.env`` file needs to be created and
the variables set appropriately. A template ``.env`` file is provided in
the source (``.env.example``), which can be copied and populated in the
copied version, ensuring the file extension is ``.env``.

4. Add country boundary data to the database

``bash npm run populateDB``

Run Web Service from Source
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: bash

    npm run dev

Running in Production mode
^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Build the service

   ``bash npm run build``

2. Start the service

``bash npm run start``

**Alternative** To run the service inside a container follow the
instructions in in the ``DEPLOYMENT.md`` guide in the source repository.
