Orchestrator
============

The orchestrator component is targeted to be a key endpoint for IoT application to interact with IoTCrawler platform.

It’s main goal of the orchestrator is to provide a subscription mechanism, which allows IoT applications to be deployed in private networks without exposing any REST-endpoints for getting notifications from MDR.

This flow is possible due to AMQP subscriptions implemented using the RabbitMQ server, running together with the orchestrator.

The Orchestrator supports NGSI-LD REST interface: all requests are redirected to MDR with some extra logic in the middle (such as tracking/caching).

This subscription mechanism allows IoT app developer to debug IoT applications using the local instance of NGSI-LD Broker (Scorpio or Jane) and then later just to switch to orchestrator’s endpoint.

IoTCrawler Client
============


The orchestrator project contains the core library (Java), which is targeted to be used in IoTCrawler applications. The idea is that standalone IoTCrawler applications would use this library and act as client to an online IoTCrawler deployment. 

Due to AMQP subscriptions mechanism the IoTCrawlerClient subscribes to the online AMQP Server and gets notifications, which placed there by the online orchestrator.

The online orchestrator is expected to receive notifications from MDR broker and put them into AMQP server. The IoTCrawlerClient subscribes to a queue associated to an exchange named as a subscription id.

This mechanism allows IoTCrawler apps to run in private networks connected to the Internet (e.g. smart home deployments, mobile apps, etc).

Code structure
============

The orchestrator project consists of a number of modules depending hierarchically (bottom modules depend on top ones):

#. `Fiware-models <https://github.com/IoTCrawler/Orchestrator/tree/master/com.agtinternational.iotcrawler.fiware-clients>`_. A library which contains classes implementing the NGSI-LD model used in NGSI-LD client library.
#. `Fiware-clients <https://github.com/IoTCrawler/Orchestrator/tree/master/com.agtinternational.iotcrawler.fiware-clients>`_. A library which contains the NGSI-LD client and a number of tests for checking its compatibility with a broker.
#. `Core <https://github.com/IoTCrawler/Orchestrator/tree/master/com.agtinternational.iotcrawler.core>`_. A library which contains the IoTCrawlerClient interface, models of the core entities (IoTStream, Sensor, Platform, etc.), two different implementations of IoTCrawlerClient. The core is targeted to be a part of client IoTCrawler application and to interact with the Orchestrator in the online IoTCrawler platform.
#. `Orchestrator <https://github.com/IoTCrawler/Orchestrator/tree/master/com.agtinternational.iotcrawler.orchestrator>`_ - A standalone standalone component running in the IoTCrawler platform.

Build
============
The orchestrator and it's supplementary libraries be built using the following command:

`sh make.sh install`

During the build process all the modules are will be installed installed into a local maven repository.

Deployment
============
The orchestrator is deployable as a docker container together with a number of assisting services (such as Redis and RabbitMQ).

A docker image for deployment can be build by the following command:

`sh make.sh build-image`

.. note::  A Google's Jib maven plugin is used for building image, so there is no traditional Dockerfile. `docker-compose build orchestrator` would not work.

A `docker-compose file <https://github.com/IoTCrawler/Orchestrator/blob/master/com.agtinternational.iotcrawler.orchestrator/docker-compose.yml>`_ is targeted for help with local running and debugging process. 

A `helm chart <https://github.com/IoTCrawler/Orchestrator/tree/master/chart>`_ describes the orchestrator and its components to be deployed on Kubernetes cluster.

A `gitlab CI configuration <https://github.com/IoTCrawler/Orchestrator/blob/master/.gitlab-ci.yml>`_ describes the building process deployment flow.

Configuration
============

The orchestrator component is configured via a number of environment variables, which can be found in a docker-compose file:

#. **IOTCRAWLER_RABBIT_HOST** - host address of AMQP server 
#. **IOTCRAWLER_REDIS_HOST** - host address of Redis server (used for mainain info about already running subscriptions).
#. **NGSILD_BROKER_URL** - URL to NGSI-LD endpoint (MDR).
#. **HTTP_SERVER_PORT** - port, on which orchestrator should listen incoming REST queries (NGSI-LD queries from apps and notifications from a broker).
#. **HTTP_REFERENCE_URL** - URL of orchestrator's endpoint to which notifications would be sent.
#. **VERSION** - for debug purposes during deployment. Automatically taken for the commit ID during image build.