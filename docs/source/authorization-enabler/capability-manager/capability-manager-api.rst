Capability Manager REST API
===========================
This section defines all REST APIs supported by Capability Manager.

.. contents:: Table of contents
   :local:
   :backlinks: none
   :depth: 3


Obtain Capability Token
+++++++++++++++++++++++

.. http:post:: /

   Obtain Capability Token.

   :reqheader Content-Type: application/json

   :<json string token: subject of the resource’s request. In DCapBAC scenario, it could correspond with a token (IDM-KeyRock). For example: "753f103c-d8e5-4f4e-8720-13d5e2f55043"
   :<json string de: endpoint of the resource’s request (protocol+IP+PORT). In DCapBAC scenario, it corresponds with PEP-Proxy component. For example: "https://153.55.55.120:2354"
   :<json string ac: method of the resource’s request ("POST", "GET", "PATCH"...)
   :<json string re: path of the resource request. For example: "/ngsi-ld/v1/entities/urn:ngsi-ld:Sensor:humidity.201"

   **Example request**:

   .. tabs::

      .. code-tab:: bash
 
         $ curl --location --request POST 'https://{{CapMan-IP}}:{{CapMan-Port}}/' \
           --header 'Content-Type: application/json' \
           --data-raw '{"token": "753f103c-d8e5-4f4e-8720-13d5e2f55043", "de": "https://153.55.55.120:2354", "ac": "GET", "re": "/ngsi-ld/v1/entities/urn:ngsi-ld:Sensor:humidity.201" }'

   **Example response**:

   .. sourcecode:: json

      {
          "id": "nlqfnfa6nqrlbh9h7tigg28ga1",
          "ii": 1586166961,
          "is": "capabilitymanager@odins.es",
          "su": "Peter",
          "de": "https://153.55.55.120:2354",
          "si": "MEUCIEEGwsTKGdlEeUxZv7jsh0UdWoFLud3uqpMDvnlT+GD7AiEAmwEu0FHuG+XyRi9BEAMaVPBIqRvOJlSIBkBT3K7LHCw=",
          "ar": [
            {
              "ac": "GET",
              "re": "/ngsi-ld/v1/entities/urn:ngsi-ld:Sensor:humidity.201"
            }
          ],
          "nb": 1586167961,
          "na": 1586177961
      }
      
   :statuscode 200: no error
   :statuscode 401: Unauthorized
   :statuscode 500: Can't generate capability token

Test Capability Manager is running
++++++++++++++++++++++++++++++++++

.. http:get:: /

   Test Capability Manager is running.

   **Example request**:

   .. tabs::

      .. code-tab:: bash
 
         $ curl --location --request GET 'https://{{CapMan-IP}}:{{CapMan-Port}}/'

   :statuscode 200: Component is running.