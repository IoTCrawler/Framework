Ranking REST API
================

Documentation of the Ranking REST API.

Obtain entities by type
+++++++++++++++++++++++

.. http:get:: /ngsi-ld/v1/entities

   Retrieve a list of all the entities.

   :query string type: entity type code as ``http://example.org/vehicle/Vehicle``, ``http://www.w3.org/2003/01/geo/wgs84_pos%23Point``, ``indexing``, etc.
   :query string weights: asdf

   **Example request**:

   .. tabs::

      .. code-tab:: bash
 
         $ curl --location --request GET 'http://{{broker-host}}/ngsi-ld/v1/entities/?type=http://example.org/vehicle/Vehicle'
 
      .. code-tab:: python
 
         import requests
         url = "http://metadata-repository-scorpiobroker.35.241.228.250.nip.io/ngsi-ld/v1/entities/?type=indexing"
         payload = {}
         headers= {}
         response = requests.request("GET", url, headers=headers, data = payload)
         print(response.text.encode('utf8'))
     
      .. code-tab:: js
 
         var request = require('request');
         var options = {
           'method': 'GET',
           'url': 'http://metadata-repository-scorpiobroker.35.241.228.250.nip.io/ngsi-ld/v1/entities/?type=indexing',
           'headers': {
           }
         };
         request(options, function (error, response) {
           if (error) throw new Error(error);
           console.log(response.body);
         });

   **Example response**:

   .. sourcecode:: json

      [
        {
          "id": "urn:ngsi-ld:Vehicle:TEST1",
          "type": "http://example.org/vehicle/Vehicle",
          "http://example.org/vehicle/brandName": {
            "type": "Property",
            "value": "Mercedes"
          },
          "http://example.org/vehicle/speed": {
            "type": "Property",
            "value": 80
          },
          "location": {
            "type": "GeoProperty",
            "value": {
              "type": "Point",
              "coordinates": [
                -1.1336517,
                37.9894006
              ]
            }
          },
          "@context": [
            "https://uri.etsi.org/ngsi-ld/v1/ngsi-ld-core-context.jsonld"
          ]
        }
      ]

   :resheader Content-Type: application/ld+json
      
   :statuscode 200: no error
