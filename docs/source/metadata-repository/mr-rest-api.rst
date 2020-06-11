MetaData REST API
=================
This section defines all REST APIs supported by MetaData Repository.

.. contents:: Table of contents
   :local:
   :backlinks: none
   :depth: 3


Projects list
+++++++++++++

.. http:get:: /ngsi-ld/v1/entities

    Retrieve a list of all the projects for the current logged in user.

    :query string type: entity type code as ``http://www.w3.org/2003/01/geo/wgs84_pos%23Point``, ``indexing``, etc.

    **Example request**:

    .. tabs::

        .. code-tab:: bash

            $ curl https://{{broker-host}}/ngsi-ld/v1/entities?type=http://example.org/vehicle/Vehicleg/api/v3/projects/

        .. code-tab:: python

            import requests
            URL = 'https://{{broker-host}}/ngsi-ld/v1/entities?type=http://example.org/vehicle/Vehicleg/api/v3/projects/'
            response = requests.get(URL)
            print(response.json())

    **Example response**:

    .. sourcecode:: json

        [
          {
            "id": "urn:ngsi-ld:Vehicle:A100",
            "type": "http://example.org/vehicle/Vehicle",
            "http://example.org/common/isParked": {
              "type": "Relationship",
              "http://example.org/common/providedBy": {
                "type": "Relationship",
                "object": "urn:ngsi-ld:Person:Bob"
              },
              "object": "urn:ngsi-ld:OffStreetParking:Downtown1",
              "observedAt": "2017-07-29T12:00:04Z"
            },
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
                  -8.5,
                  41.2
                ]
              }
            },
            "@context": [
              "https://schema.lab.fiware.org/ld/context"
            ]
          }
        ]
