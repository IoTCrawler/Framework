Sensor Integration
==================
In this section we provide and example on how to include sensor data into the IoTCrawler framework. The sourcecode for this example can be accessed ad https://github.com/IoTCrawler/iotcrawler-samples/tree/master/sensorintegration.


This example 'translates' CityProbe date available at
https://www.opendata.dk/city-of-aarhus/bymiljo-aarhus-cityprobe into the
IoTCrawler information model. The information model can be found at ...

Example data (CityProbe)
------------------------

Let's have a look at the data provided by a CityProbe sensor in Aarhus.
It can be accessed with:
https://admin.opendata.dk/api/3/action/datastore\_search?offset=792392&resource\_id=7e85ea85-3bde-4dbf-944b-0360c6c47e3b&limit=1.
For demonstration we have set the limit to 1.

::

    {
      "help": "https://admin.opendata.dk/api/3/action/help_show?name=datastore_search",
      "success": true,
      "result": {
        "include_total": true,
        "resource_id": "7e85ea85-3bde-4dbf-944b-0360c6c47e3b",
        "fields": [
          {
            "type": "int",
            "id": "_id"
          },
          {
            "info": {
              "notes": "St\u00f8j i et JSON-objekt med hhv. gennemsnit, minimum og maksimumsv\u00e6rdier\r\n* Enhed: dB SPL",
              "type_override": "",
              "label": "St\u00f8j"
            },
            "type": "json",
            "id": "noise"
          },
          {
            "info": {
              "notes": "Kulilte/carbonmonoxid m\u00e5lt i et 12-bit interval (0 - 4095) p\u00e5 en 3.3V linje. \r\nOpl\u00f8sningen er 0.8 mV per enhed. Modstanden formindskes ved tilstedev\u00e6relsen af CO og carbonhydrider.\r\n",
              "type_override": "",
              "label": "Kulilte"
            },
            "type": "int4",
            "id": "CO"
          },
          {
            "info": {
              "notes": "* Enhed: Celcius\r\n* Pr\u00e6cision: \u00b10.5\u00b0C\r\n",
              "type_override": "",
              "label": "Temperatur"
            },
            "type": "float8",
            "id": "temperature"
          },
          {
            "info": {
              "notes": "* Enhed: \u03bcg/m3",
              "type_override": "",
              "label": "Partikelforurening (10 \u00b5m)"
            },
            "type": "int4",
            "id": "PM10"
          },
          {
            "info": {
              "notes": "Batterikapacitet i procent\r\nEnheden oplades ved hj\u00e6lp af et solpanel",
              "type_override": "",
              "label": "Batterikapacitet"
            },
            "type": "float8",
            "id": "battery"
          },
          {
            "info": {
              "notes": "Regnintensitet i et JSON-objekt med hhv. gennemsnit, minimum og maksimumsv\u00e6rdier i dB SPL.\r\nM\u00e5lemetoden er en mikrofon under en polycarbonath\u00e6tte, som m\u00e5ler peak amplitude og frekvensen af dr\u00e5ber, som rammer toppen. P\u00e5 Open Data DK er v\u00e6rdierne r\u00e5 og ikke analyseret.",
              "type_override": "",
              "label": "Regnintensitet"
            },
            "type": "json",
            "id": "rain"
          },
          {
            "info": {
              "notes": "Enhed: %RH\r\nPr\u00e6cision: \u00b13 %RH\r\n",
              "type_override": "",
              "label": "Luftfugtighed"
            },
            "type": "float8",
            "id": "humidity"
          },
          {
            "info": {
              "notes": "Lysintensitet m\u00e5lt i lux",
              "type_override": "",
              "label": "Dagslys"
            },
            "type": "int4",
            "id": "illuminance"
          },
          {
            "info": {
              "notes": "Lufttryk m\u00e5lt i hPa\r\nPr\u00e6cision: \u00b11.0 hPa",
              "type_override": "",
              "label": "Lufttryk"
            },
            "type": "float8",
            "id": "pressure"
          },
          {
            "info": {
              "notes": "Tidsstempel for m\u00e5lingen i UTC og ISO 8601-format",
              "type_override": "",
              "label": "Tidsstempel"
            },
            "type": "text",
            "id": "published_at"
          },
          {
            "info": {
              "notes": "Enhed: \u03bcg/m3",
              "type_override": "",
              "label": "Partikelforurening (2.5 \u00b5m)"
            },
            "type": "int4",
            "id": "PM2.5"
          },
          {
            "info": {
              "notes": "ID for den p\u00e5g\u00e6ldende enhed, som har foretaget m\u00e5lingen.",
              "type_override": "",
              "label": "Enhedsid"
            },
            "type": "text",
            "id": "deviceid"
          },
          {
            "info": {
              "notes": "Kv\u00e6lstofdioxid m\u00e5lt i et 12-bit interval (0 - 4095) p\u00e5 en 3.3V linje. \r\nOpl\u00f8sningen er 0.8 mV per enhed. Modstanden for\u00f8ges ved tilstedev\u00e6relsen af CO og carbonhydrider.",
              "type_override": "",
              "label": "Kv\u00e6lstofdioxid"
            },
            "type": "int4",
            "id": "NO2"
          },
          {
            "type": "int4",
            "id": "firmware_version"
          },
          {
            "type": "text",
            "id": "device_id"
          }
        ],
        "records_format": "objects",
        "records": [
          {
            "_id": 794720,
            "noise": "{\"max\": \"67.46\", \"average\": \"61.57\", \"min\": \"56.86\"}",
            "CO": 825,
            "temperature": 0,
            "PM10": 0,
            "battery": 89.59,
            "rain": "{\"max\": \"492\", \"average\": \"215.05\", \"min\": \"96\"}",
            "humidity": 0,
            "illuminance": 49595,
            "pressure": 0,
            "published_at": "2020-06-17T10:20:35.255Z",
            "PM2.5": 0,
            "deviceid": "20004c000d50483553343720",
            "NO2": 889,
            "firmware_version": 49,
            "device_id": null
          }
        ],
        "limit": 1,
        "offset": 792392,
        "_links": {
          "start": "/api/3/action/datastore_search?limit=1&resource_id=7e85ea85-3bde-4dbf-944b-0360c6c47e3b",
          "prev": "/api/3/action/datastore_search?offset=792391&limit=1&resource_id=7e85ea85-3bde-4dbf-944b-0360c6c47e3b",
          "next": "/api/3/action/datastore_search?offset=792393&limit=1&resource_id=7e85ea85-3bde-4dbf-944b-0360c6c47e3b"
        },
        "total": 792920
      }
    }

The provided data contains some meta information within the fields list.
The data itself is contained in the records list. In our case there is
just one entry because of the set limit. So let us just have a look at
the "data":

::

    {
        "_id": 794720,
        "noise": "{\"max\": \"67.46\", \"average\": \"61.57\", \"min\": \"56.86\"}",
        "CO": 825,
        "temperature": 0,
        "PM10": 0,
        "battery": 89.59,
        "rain": "{\"max\": \"492\", \"average\": \"215.05\", \"min\": \"96\"}",
        "humidity": 0,
        "illuminance": 49595,
        "pressure": 0,
        "published_at": "2020-06-17T10:20:35.255Z",
        "PM2.5": 0,
        "deviceid": "20004c000d50483553343720",
        "NO2": 889,
        "firmware_version": 49,
        "device_id": null
    }

As can be seen the data contains noise, CO, temperature, PM10, battery,
rain, humidity, illuminance, pressure, PM2.5, and NO2 as data fields.
Besides that deviceid contains the relation to the measurung sensor and
published\_at containes a timestamp of the measurement. The other fields
are not used in this example.

Translation into IoTCrawler model
---------------------------------

In the IoTCrawler information modell (cf. ...) we have to split the
provided information from the CityProbe dataset. In our example we will
have

- 1 Platform hosting 11 sensors
- 11 Sensors (one for each datafield) 
- 11 IoTStreams (one for each Sensor) 
- 11 ObservableProperties (one for each Sensor) 
- 11 StreamObservations (one for each Sensor)

With the help of the provided script these entities are created. For details please have a look at https://github.com/IoTCrawler/iotcrawler-samples/blob/master/sensorintegration/main.py

Connection to MDR/Broker
------------------------

The translated data is stored into the MDR by using the standardise
NGSI-LD API (see `NGSI-LD
API <https://www.etsi.org/deliver/etsi_gs/CIM/001_099/009/01.02.01_60/gs_CIM009v010201p.pdf>`__)
In the example script this is done in a threaded way to avoid blocking.
The broker returns several HTTP status codes for feedback while accessing
its interface at 

.. http:get:: /ngsi-ld/v1/entities/:

  :statuscode 201: entity was successfully created 
  :statuscode 400: bad request, the entity is probably not in ngsi-ld format
  :statuscode 409: the entity already exists
  :statuscode 500: internal server error

In case of a 409 status code we have to PATCH the entity as it is
already existing. The interface will change to
/ngsi-ld/v1/entities/ENTITYID/attrs/ were ENTITYID has to be replaced by
the entity that should be updated. Additionally the id and type has to
be deleted from the provided entity in NGSI-LD format. Within the script
this is done automatically.

Sourcecode
----------
The sourcecode for the example can be found at https://github.com/IoTCrawler/iotcrawler-samples/tree/master/sensorintegration