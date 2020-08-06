Ranking REST API
================

Documentation of the Indexing REST API.

Obtain entities by type
+++++++++++++++++++++++

.. http:get:: /api/health

   Status of api health

   **Example request**:

   .. tabs::

      .. code-tab:: bash
 
         $ curl --location --request GET 'https://{{indexing-host}}/api/health'

   **Example response**:

   .. sourcecode:: json

      {
        "status": "UP"
      } 

   :resheader Content-Type: application/json
      
   :statuscode 200: no error
