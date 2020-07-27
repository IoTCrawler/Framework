Ranking
=======

The Ranking component facilitates ranking mechanism for IoT resources. Ranking and resource selection rely on the registry built (and constantly updated) by crawling and indexing methods. The purpose of Ranking is to aid users and applications to not only find a set of resources relevant to their needs, but also to select the best or most appropriate one(s) from that set. There are multiple criteria for ranking IoT resources such as data type, proximity, latency, availability. The Ranking component supports application-dependent, multi-criteria ranking.

Integration into IoTCrawler Framework
-------------------------------------
Within the IoTCrawler framework the ranking component can be used by the orchestrator component to facilitate entity discovery. The ranking component relies on a NGSI-LD compliant endpoint as a backend, which is often times the :doc:`/indexing/indexing` component but could also be any NGSI-LD broker.

Ranking score computation
-------------------------
The ranking score is computed by a weighted sum function. Formally, for NGSI-LD properties :math:`p_1 \ldots p_n` and corresponding weights :math:`w_1 \ldots w_n` the ranking score :math:`r` is computed as following:

.. math:: r = \sum_{i}^{} p_i w_i

For the ranking component the weights and NGSI-LD property names for the values have to be supplied by the query. 

Example for multi-criteria ranking
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

We want to rank NGSI-LD entities by the two (abbreviated) properties completeness and artificiality and weigh completeness 4 times more important than artificiality. Both NGSI-LD properties have values between 0 and 1 and we would like to get a ranking score also between 0 and 1. To achieve this the weights for both properties must add up to 1, therefore we fix the weight for completeness as 0.8 and the weight for artificiality as 0.2. If we now have two entities in to rank (with 'switched' values for completeness and artificiality), then the ranking scores are computed as follows:

+---------------+--------------+---------------+---------------+
| entity        | completeness | artificiality | ranking score |
|               | value        | value         | value         |
+===============+==============+===============+===============+
| entity 1      |         0.88 |          0.92 |         0.888 |
+---------------+--------------+---------------+---------------+
| entity 2      |         0.92 |          0.88 |         0.912 |
+---------------+--------------+---------------+---------------+

Due to the higher weight of the completeness property, the ranking score favors entity 2 with the higher completeness value.

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
