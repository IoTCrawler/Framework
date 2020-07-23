IdM-Keyrock REST API
====================
This section defines specific IdM-Keyrock requests required in IotCrawler environment. Further information can be found in the Keyrock Apiary (https://keyrock.docs.apiary.io).

.. contents:: Table of contents
   :local:
   :backlinks: none
   :depth: 3


Generate/Obtain a new IdM Token
+++++++++++++++++++++++++++++++

.. http:post:: /v1/auth/tokens

   Generate/Obtain a new IdM Token.

   :reqheader Content-Type: application/json

   :<json string name: IdM-Keyrock user. For example: "admin@test.com"
   :<json string password: IdM-Keyrock user password. For example: "1234"

   **Example request**:

   .. tabs::

      .. code-tab:: bash
 
         $ curl --location --request POST 'https://{{IdM-IP}}:{{IdM-Port}}/v1/auth/tokens' \
            --header 'Content-Type: application/json' \
            --data-raw '{
              "name": "admin@test.com",
              "password": "1234"
            }'

   **Example response**:

   .. sourcecode:: json

      {
          "token": {
              "methods": [
                  "password"
              ],
              "expires_at": "2020-07-21T10:02:19.256Z"
          },
          "idm_authorization_config": {
              "level": "advanced",
              "authzforce": true
          }
      }
   :resheader X-Subject-Token: IdM-Keyrock token. For example: "cf41496e-d9b2-4f1f-8cba-f4efb3bf9abe"
   :resheader Content-Type: application/json
   :statuscode 201: Created
   :statuscode 401: Unauthorized

Obtain the IdM Token information
++++++++++++++++++++++++++++++++

.. http:get:: /v1/auth/tokens

   Obtain the IdM Token information.

   **Example request**:

   .. tabs::

      .. code-tab:: bash
 
         $ curl --location --request GET 'https://{{IdM-IP}}:{{IdM-Port}}/v1/auth/tokens' \
                --header 'X-Auth-token: cf41496e-d9b2-4f1f-8cba-f4efb3bf9abe' \
                --header 'X-Subject-token: cf41496e-d9b2-4f1f-8cba-f4efb3bf9abe'

   **Example response**:
   .. sourcecode:: json

      {
          "access_token": "cf41496e-d9b2-4f1f-8cba-f4efb3bf9abe",
          "expires": "2020-07-21T10:47:23.000Z",
          "valid": true,
          "User": {
              "scope": [],
              "id": "admin",
              "username": "admin",
              "email": "admin@test.com",
              "date_password": "2019-10-22T12:45:58.000Z",
              "enabled": true,
              "admin": true
          }
      }

   :resheader Content-Type: application/json
   :statuscode 200: OK.
   :statuscode 401: Unauthorized