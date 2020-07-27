Seach-enabler
============

The search-enabler component is targeted to REST endpoint for GraphQL queries coming from IoT applications.

For creating, debugging and testing GraphQL queries a GraphiQL GUI environment provided. 

See the `tutorial <../tutorials/graphql_search.html>`_ for more details.

Build
########
The search-enabler is implemented using as IoTCrawlerClient provided by a core library (see `Orchestrator <../orchrestrator/orchrestrator.html>`_ for more details). As a result it builds orchestrator library during the build process.

`sh make.sh install`

During the build process all the modules are will be installed installed into a local maven repository.

Deployment
########
The search-enabler is deployable as a docker container.

A docker image for deployment can be build by the following command:

`sh make.sh build-image`

.. note::  A Google's Jib maven plugin is used for building image, so there is no traditional Dockerfile. Use build-command instead.

A `helm chart <https://github.com/IoTCrawler/Search-Enabler/tree/master/chart>`_ configures the search-enabler to be deployed on Kubernetes cluster.

A `gitlab CI configuration <https://github.com/IoTCrawler/Search-Enabler/blob/master/.gitlab-ci.yml>`_ configures the building process deployment flow.

Configuration
########

#. **IOTCRAWLER_ORCHESTRATOR_URL** - URL of NGSI-LD endpoint (orchestrator or MDR Broker).
#. **VERSION** - for debug purposes during deployment. Automatically taken for the commit ID during image build.
          