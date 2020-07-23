======================
Virtual Sensor Creator
======================

.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

This component is responsible for the creation of Virtual Sensors in the IoTCrawler framework. A Virtual Sensor can be used to replace a broken sensor. To do this, the component searches for other data sources within a given radius. It then calculates if the data by broken sensor correlates with the other data source candidates. Candidates with a high correlation are then used to train various ML models. Via grid search the best suitable model is selected for the Virtual Sensor. The model is then used to predict new virtual *StreamObservations*, which published via the MDR.


Usage
-----

The component uses a HTTP interface to deploy and undeploy Virtual Sensors and is intended to be called by the Fault Detection component.

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
This method can be used to replace a broken sensor. The request requires the ID of the broken sensor to replace. The optional parameter **maxDistance** can be used to limit the radius the component will search for data sources that may be used as input for the Virtual Sensor (default 20km). With the optional parameter **onlySameObservations** the Virtual Sensor Creator will look only for other data sources measuring the same physical phenomena, identified by the *ObservableProperty's* label. The found data sources, or their data to be precise, is tested if it correlates with the data of the broken sensor, before training the ML model. Not correlating sources are not considered in the training. With **limitSourceSensors**, the number of data sources can be limited further. This may be necessary if data sources have a high number of historic data samples, since it can cause a high strain on computational resources and also require more computational time throughout the Virtual Sensor deployment pipeline, i.e. from the preprocessing of data to the training of the model.


This may be necessary if data sources have a high number of historic data samples, since their temporal alignment to form the training data requires a lot of time and memory. This limit takes effect before the test for correlations, thus the final number of contributing data sources may be even smaller.

If correlating data sources are found, this method returns the NGSI-LD description for the created Virtual Sensor. At this point the training of the ML model starts. After this, the component subscribes to *StreamObservations* of the contributing sensors. The predictions of the Virtual Sensor are done in a fixed update interval (configurable via the **updateInterval** parameter). If not all contributing sensors have published a new *StreamObservation* until then, the last known value is used for the prediction.

.. http:get:: /api/replaceBrokenSensor/

with payload

::

    {
      "sensorID" : <The ID of the broken sensor>,
      "maxDistance": <The maximum distance in meter to search for contributing sensors. Integer, default 20000.>,
      "onlySameObservations": <Consider only sensors that measure the same observation as the broken sensor. Boolean, default true.>,
      "limitSourceSensors": <Limit the number of contributing sensors. Interger, default 8.>,
      "updateInterval": <Number of seconds, in which the Virtual Sensor shall predict a new value>
    }


The :red:`data` field in the response will contain the NGSI-LD description for the new Virtual Sensor.

**Please note:**  although this API method is named *replace* BrokenSensor, the original sensor is not removed from the IoTCrawler system.

Deploy a new Virtual Sensor
---------------------------

:red:`This method is not fully implemented!`

Instead of replacing a broken sensor this component also allows to deploy a Virtual Sensor for locations, where no real sensor is present. For this the following API method can be used. It must include the parameter **location** where the new Virtual Sensor shall be deployed as well as the ID of an *ObservableProperty* (parameter **propertyID**) to indicate what physical phenomena shall be 'measured'. The rest of the optional parameters have the same meaning as for the replaceBrokenSensor method. The Virtual Sensor will use linear regression to predict new *StreamObservations*.

.. http:get:: /api/deployVirtualSensor/

with payload

::

    {
      "location" : [<latitude>, <longitude>, <altitude>],
      "propertyID": <The ID of an ObservableProperty the new sensor shall measure>
      "maxDistance": <The maximum distance in meter to search for contributing sensors. Integer, default 20000.>,
      "onlySameObservations": <Consider only sensors that measure the same observation as the broken sensor. Boolean, default true.>,
      "limitSourceSensors": <Limit the number of contributing sensors. Interger, default 8.>,
      "updateInterval": <Number of seconds, in which the Virtual Sensor shall predict a new value>
    }


Stop a Virtual Sensor
---------------------
This method can be used to stop an previously deployed Virtual Sensor, identified by its ID as returned by the deployment methode. If no Virtual Sensor with the given ID (parameter **sensorID**) exists this method returns an error. Otherwise the Virtual Sensor is stopped and the Virtual Sensor Creator component will delete the related entries in MDR, such as *Sensor*, *Platform* or *StreamObservations*. The un-deployment is triggered by a HTTP request to:

.. http:get:: /api/stopVirtualSensor

with payload

::

  {
    "sensorID" : <The ID of the Virtual Sensor to stop>
  }


List of Virtual Sensors deployed
--------------------------------
To get a list of all deployed Virtual Sensors issue the following HTTP request:

.. http:get:: /api/list

The response will be a JSON dictionary object with the IDs of the Virtual Sensors as key and the NGSI-LD description of the Virtual Sensor as value. For example:

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


Build a Docker image
--------------------
Change into the VirtualSensor directory and execute the script **build.sh**. This creates a Docker image tagged **vs_creator:1**.

Run in Docker container
-----------------------
This repository includes a script to start the previously created image named **run.sh**. For the component to be able to interact with other IoTCrawler components, two environment variables need to be set. The first one is called BROKER_ADDRESS and contains the address of the MDR in the form <IP|DNS name>:<PORT> (e.g. "155.54.95.248:9090"). The second variable is named CALLBACK_ADDRESS and contains the address of the Virtual Sensor Creator component to allow the MDR component to notify this component about new *StreamObservations*. You can test if the component is running by calling http://localhost:8080/api/status .

Sourcecode
----------
The source code for the example can be found at https://github.com/IoTCrawler/

Requirements
------------
For a list of required Python modules see requirements.txt in the source repository.
