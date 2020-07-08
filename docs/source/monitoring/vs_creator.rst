Virtual Sensor Creator
======================

This component is responsible for the creation of Virtual Sensors in the IoTCrawler framework. The component uses a HTTP interface to deploy and undeploy virtual sensors.

Usage:
------

All requests are replied with a JSON response in the following structure:

::

  {
      "status": "ok" | "error",
      "success": true | false,
      "description": <error description if not successful>,
      "data": <Optionally, the data in case of success>
  }




Replace a (broken) Sensor with a Virtual Sensor
-----------------------------------------------
.. http:get:: /api/replaceBrokenSensor/

with payload

::

    {
      "sensorID" : <The ID of the broken sensor>,
      "maxDistance": <The maximum distance in meter to search for contributing sensors. Integer, default 20000.>,
      "onlySameObservations": <Consider only sensors that measure the same observation as the broken sensor. Boolean, default true.>,
      "limitSourceSensors": <Limit the number of contributing sensors. Interger, default 8.>,
      "": [<>]
    }


  The 'data' field in the response will contain the NGSI-LD description for the new virtual sensor.

Stop a Virtual Sensor
---------------------
.. http:get:: /api/stopVirtualSensor

with payload

::

  {
    "sensorID" : <The ID of the virtual sensor to stop>
  }


List of Virtual Sensors deployed
--------------------------------
.. http:get:: /api/list

  Response:
  A JSON dict with the IDs of the virtual sensors as key and the NGSI-LD description of the virtual sensor as value. For example:

::

  {
      "status": "ok",
      "success": true,
      "description": "",
      "data": {
          "urn:ngsi-ld:Sensor:SolarPowerAarhus:492:currentProduction:VS": {
              "id": "urn:ngsi-ld:Sensor:SolarPowerAarhus:492:currentProduction:VS",
              "type": "http://www.w3.org/ns/sosa/Sensor",
              "http://www.w3.org/ns/sosa/isHostedBy": {
                  "type": "Relationship",
                  "object": "urn:ngsi-ld:Platform:SolarPowerAarhus:492:VS"
              },
              "http://www.w3.org/ns/sosa/madeObservation": {
                  "type": "Relationship",
                  "object": "urn:ngsi-ld:StreamObservation:SolarPowerAarhus:492:currentProduction:VS"
              },
              "http://www.w3.org/ns/sosa/observes": {
                  "type": "Relationship",
                  "object": "urn:ngsi-ld:ObservableProperty:SolarPowerAarhus:currentProduction"
              },
              "location": {
                  "type": "GeoProperty",
                  "value": {
                      "type": "Point",
                      "coordinates": [
                          56.253,
                          10.149
                      ]
                  }
              },
              "https://w3id.org/iot/qoi#max": {
                  "type": "Property",
                  "value": "NA"
              },
              "https://w3id.org/iot/qoi#min": {
                  "type": "Property",
                  "value": "NA"
              },
              "https://w3id.org/iot/qoi#updateinterval": {
                  "type": "Property",
                  "value": "NA",
                  "https://w3id.org/iot/qoi#unit": {
                      "type": "Property",
                      "value": "NA"
                  }
              },
              "https://w3id.org/iot/qoi#valuetype": {
                  "type": "Property",
                  "value": "NA"
              },
              "@context": [
                  "http://uri.etsi.org/ngsi-ld/v1/ngsi-ld-core-context.jsonld",
                  {}
              ]
          }
      }
  }


Run in Docker container
-----------------------

* Build the image:
  docker build -t vs_creator:1 .
* Run:
  docker run -p 8080:8080 vs_creater:1
* Test by opening http://localhost:8080/api/status

Sourcecode
----------
The sourcecode for the example can be found at https://github.com/IoTCrawler/

Dependencies
------------
See requirements.txt in the source repository.
