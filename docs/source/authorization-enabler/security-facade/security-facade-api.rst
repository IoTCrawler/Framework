Security Facade REST API
========================
This section defines all REST APIs supported by Security Facade.

.. contents:: Table of contents
   :local:
   :backlinks: none
   :depth: 3


Obtain Capability Token
+++++++++++++++++++++++

.. http:post:: /CapabilityManagerServlet/IdemixTokenIdentity

   Obtain Capability Token.

   :reqheader idemixIdentity: IdM-Keyrock user credentials. For example: {"name": "peter@odins.es","password": "iotcrawler"}
   :reqheader device: endpoint of the resource’s request (protocol+IP+PORT). In DCapBAC scenario, it corresponds with PEP-Proxy component. For example: "https://153.55.55.120:2354"
   :reqheader action: method of the resource’s request ("POST", "GET", "PATCH"...)
   :reqheader resource: path of the resource request. For example: "/ngsi-ld/v1/entities/urn:ngsi-ld:Sensor:humidity.201"

   **Example request**:

   .. tabs::

      .. code-tab:: bash
 
         $ curl --location --request POST 'https://{{Facade-IP}}:{{Facade-Port}}/CapabilityManagerServlet/IdemixTokenIdentity' \
                --header 'action: GET' \
                --header 'resource: /ngsi-ld/v1/entities/urn:ngsi-ld:Sensor:humidity.201' \
                --header 'device: https://153.55.55.120:2354' \
                --header 'idemixIdentity: {"name": "peter@odins.es","password": "iotcrawler"}'

   **Example response**:

   .. sourcecode:: json

      {
          "id": "19tp7qp5se7t27hi9lm8uc5iko",
          "ii": 1595400471,
          "is": "capabilitymanager@odins.es",
          "su": "Peter",
          "de": "https://153.55.55.120:2354",
          "si": "I3QObay3SB531ICuwisnXvhhMSjEF77ViKwZkH9ASeMgneIJjuVHx4YAyu3acys/+Jh8pK3Gwh+XC69UMZsm+SnXz+Zh0XJBpo5ZGq3DHZeayimNMW19aVlckTCGxv/YtZydbjsGbJqeKXXWQPv1tzZpHhFWKNfppr13cVON30Irmcm4nbdQp672+IFaBI6WRCrqNAtmQRPW25OqKJ1k+G+Yh4/UU06+kPRTwutBRChgX+Pl8W9vzxxBmknoMQbeJW3dn1DbfhB5zMX2Pa8uMKaufIV/r/H0R6HSZ1d33CCv7SwwVipHq8ktp2G4UEtFYALgRx2pvlTiGEqTiiWVZwu939Q3RG/wqMd8bDX6PQtexf7WMO4sbkTl1Y/65DCGODnWA1Tvwn+NDHqMLXea+cdPFpl9tPFT4FLHbt0U22x81Ks4IdqLInkjXm0gBBLIT3XbKl4UtTBTwI1LZwY7p2U+9Z/oK/M0ELIj/aoApDLWKryqDP2Fx/KWh+e5s43t+T/G5RaTv5HORP8dvTnLkrVgRuDpgbyJrLhPY7wXCeSSKYZk1+LvJKVzS8DW9bDbCFPTJTSyIXMO9VgfY8PLdlUVALOAjJZCQxVTmhnK3a4y0TVApQfp8sqFjR6dOee29wXZSZSPJpvi5j52rg/9+kdFZ+3XyKSNBeIPkx0SaIo=",
          "ar": [
            {
              "ac": "GET",
              "re": "/ngsi-ld/v1/entities/urn:ngsi-ld:Sensor:humidity.201"
            }
          ],
          "nb": 1595401471,
          "na": 1595411471
      }
      
   :statuscode 200: OK or "There was an error getting the Token." (Unauthorized)

Test Security Facade is running
+++++++++++++++++++++++++++++++

.. http:get:: /CapabilityManagerServlet/

   Test Security Facade is running.

   **Example request**:

   .. tabs::

      .. code-tab:: bash
 
         $ curl --location --request GET 'https://{{Facade-IP}}:{{Facade-Port}}/CapabilityManagerServlet/'

   :statuscode 200: Component is running. Served at: /CapabilityManagerServlet