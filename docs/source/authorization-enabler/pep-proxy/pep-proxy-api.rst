PEP-Proxy REST API
==================
This section defines all REST APIs supported by PEP-Proxy.

.. contents:: Table of contents
   :local:
   :backlinks: none
   :depth: 3


Accesing to resource
++++++++++++++++++++

The PEP-Proxy component hasn't a specific API, it uses the same API that will forward requests. The unique difference is you must add a new header `x-auth-token` where capability token must be included as a string. 

.. http:get:: /

   Example of request (GET) to forward to MDR's API.

   :reqheader x-auth-token: `Capability Token`

   **Example request**:

   .. tabs::

      .. code-tab:: bash
 
         $ curl --location --request GET 'https://{{PEP-Proxy-IP}}:{{PEP-Proxy-Port}}{{resource}}' \
          --header 'x-auth-token: {"id": "nlqfnfa6nqrlbh9h7tigg28ga1","ii": 1586166961,"is": "capabilitymanager@odins.es","su": "Peter","de": "https://153.55.55.120:2354","si": "MEUCIEEGwsTKGdlEeUxZv7jsh0UdWoFLud3uqpMDvnlT+GD7AiEAmwEu0FHuG+XyRi9BEAMaVPBIqRvOJlSIBkBT3K7LHCw=",
          "ar": [{"ac": "GET","re": "/ngsi-ld/v1/entities/urn:ngsi-ld:Sensor:humidity.201"}],"nb": 1586167961,"na": 1586177961}'

Test PEP-Proxy is running
+++++++++++++++++++++++++

.. http:get:: /

   Test PEP-Proxy is running.

   **Example request**:

   .. tabs::

      .. code-tab:: bash
 
         $ curl --location --request GET 'https://{{PEP-Proxy-IP}}:{{PEP-Proxy-Port}}/'

   **Example response**:

   :statuscode 200: Component is running.

