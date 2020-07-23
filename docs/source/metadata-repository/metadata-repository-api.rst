MetaData REST API
=================
This section shows the basic entity requests used in the REST API of the MetaData Repository. For a detail explanation, please look the ETSI spec.

.. contents:: Table of contents
   :local:
   :backlinks: none
   :depth: 3

Add entity
++++++++++

.. http:post:: /ngsi-ld/v1/entities/

   Add a new entity.

   :reqheader Content-Type: application/ld+json

   **Example request**:

   .. tabs::

      .. code-tab:: bash
 
         $ curl --location --request POST 'http://{{broker-host}}/ngsi-ld/v1/entities/' \
                --header 'Content-Type: application/ld+json' \
                --data-raw '{
                  "@context":[
                        "https://uri.etsi.org/ngsi-ld/v1/ngsi-ld-core-context.jsonld",
                        {
                            "Vehicle": "http://example.org/vehicle/Vehicle",
                            "brandName": "http://example.org/vehicle/brandName",
                            "speed": "http://example.org/vehicle/speed"
                        }
                  ],
                  "id":"urn:ngsi-ld:Vehicle:TEST1",
                  "type":"Vehicle",
                  "brandName":{
                    "type":"Property",
                    "value":"Mercedes"
                  },
                  "speed":{
                    "type":"Property",
                    "value":80
                  },
                  "location": {
                        "type": "GeoProperty",
                        "value": { "type": "Point", "coordinates": [ -1.1336517, 37.9894006 ] }
                  }
                }'

      
   :statuscode 201: Created


Obtain entities by type
+++++++++++++++++++++++

.. http:get:: /ngsi-ld/v1/entities

   Retrieve a list of all the entities.

   :query string type: entity type code as ``http://example.org/vehicle/Vehicle``, ``http://www.w3.org/2003/01/geo/wgs84_pos%23Point``, ``indexing``, etc.

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

Obtain entity by id
+++++++++++++++++++

.. http:get:: /ngsi-ld/v1/entities/(str:get_id)

   Retrieve an entity by identifier.

   :param get_id: get's unique id
   :type get_id: str

   **Example request**:

   .. tabs::

      .. code-tab:: bash
 
         $ curl --location --request GET 'http://{{broker-host}}/ngsi-ld/v1/entities/urn:ngsi-ld:Vehicle:TEST1'

   **Example response**:

   .. sourcecode:: json

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

   :resheader Content-Type: application/ld+json
      
   :statuscode 200: no error
   :statuscode 404: not found


Update entity
+++++++++++++

.. http:patch:: /ngsi-ld/v1/entities/(str:patch)/attrs

   Update entity.

   :param patch: patch's unique id
   :type patch: str

   :reqheader Content-Type: application/ld+json

   **Example request**:

   .. tabs::

      .. code-tab:: bash
 
         $ curl --location --request PATCH 'http://{{broker-host}}/ngsi-ld/v1/entities/urn:ngsi-ld:Vehicle:TEST1/attrs' \
              --header 'Content-Type: application/ld+json' \
              --data-raw '{
                  "@context":[
                      "https://uri.etsi.org/ngsi-ld/v1/ngsi-ld-core-context.jsonld",
                      {
                          "Vehicle": "http://example.org/vehicle/Vehicle",
                          "brandName": "http://example.org/vehicle/brandName",
                          "speed": "http://example.org/vehicle/speed"
                      }
                  ],
                "brandName":{
                     "type":"Property",
                     "value":"Seat"
                  },
                  "speed": {
                      "type": "Property",
                      "value": 5
                  }
                  
              }'
 
   :statuscode 204: No content, no error
   :statuscode 404: not found

Delete entity
+++++++++++++

.. http:delete:: /ngsi-ld/v1/entities/(str:delete_id)

   Remove an entity by identifier.

   :param delete_id: delete's unique id
   :type delete_id: str

   **Example request**:

   .. tabs::

      .. code-tab:: bash
 
         $ curl --location --request DELETE 'http://{{broker-host}}/ngsi-ld/v1/entities/urn:ngsi-ld:Vehicle:TEST1'
 
   :statuscode 204: No content, no error
   :statuscode 404: not found