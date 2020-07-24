Ranking
=======

The Ranking component facilitates ranking mechanism for IoT resources. Ranking and resource selection rely on the registry built (and constantly updated) by crawling and indexing methods. The purpose of Ranking is to aid users and applications to not only find a set of resources relevant to their needs, but also to select the best or most appropriate one(s) from that set. There are multiple criteria for ranking IoT resources such as data type, proximity, latency, availability. The Ranking component supports application-dependent, multi-criteria ranking.

Integration into IoTCrawler Framework
-------------------------------------
Within the IoTCrawler framework the ranking component can be used by the orchestrator component to facilitate entity discovery. The ranking component relies on a NGSI-LD compliant endpoint as a backend, which is often times the :doc:`/indexing/indexing` component but could also be any NGSI-LD broker.

Ranking score computation
-------------------------
The ranking score is computed by a weighted sum function. The weights and NGSI-LD property names for the values have to be supplied by the query.

Setup
-----
The Ranking component is provided as Docker image from Docker Hub (<TODO>: add docker hub URL), it only needs a configuration file.

For the configuration several environment variables (such as the backend NGSI-LD endpoint) have to be set.
Either prepare a ``config.env`` file, similar to sample.env_, or set the environment variables as in sample.env_ on the command line when starting the docker container.

Eventually run the following command to deploy the Ranking component:

.. code:: bash

   docker run -p 3003:3003 --env-file=config.env iotcrawler-ranking   

REST API
--------
Please refer to the :doc:`ranking-api` documentation.

Details and code
----------------
Please refer to the `Ranking Github repository`_ for further details (e.g., how to build your own custom Docker image) and source code of the ranking component.

.. _sample.env: https://github.com/IoTCrawler/Ranking/blob/master/sample.env
.. _Ranking Github repository: https://github.com/IoTCrawler/Ranking
