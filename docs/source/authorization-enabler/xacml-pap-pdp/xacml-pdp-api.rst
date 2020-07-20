XACML - PDP REST API
====================
This section defines all REST APIs supported by XACML - PDP.

.. contents:: Table of contents
   :local:
   :backlinks: none
   :depth: 3


Obtain Verdict
+++++++++++++++

.. http:post:: /XACMLServletPDP/

   Obtain Verdict.

   :reqheader Content-Type: text/plain

   :<json string subject: subject of the resource’s request. In DCapBAC scenario, it could correspond with a username (IDM). For example: "Peter"
   :<json string resource: endpoint + path of the resource’s request (protocol+IP+PORT+path). For example: "https://153.55.55.120:2354/ngsi-ld/v1/entities/urn:ngsi-ld:Sensor:humidity.201".  In DCapBAC scenario, endpoint corresponds with the PEP-Proxy one.
   :<json string action: method of the resource’s request ("POST", "GET", "PATCH"...)

   **Example request**:

   .. tabs::

      .. code-tab:: bash
 
         $  curl --location --request POST 'http://{{XACML-PDP-IP}}:{{{XACML-PDP-Port}}/XACMLServletPDP/' \
            --header 'Content-Type: text/plain' \
            --data-raw '<Request xmlns="urn:oasis:names:tc:xacml:2.0:context:schema:os">
               <Subject SubjectCategory="urn:oasis:names:tc:xacml:1.0:subject-category:access-subject">
                   <Attribute AttributeId="urn:oasis:names:tc:xacml:2.0:subject:role" DataType="http://www.w3.org/2001/XMLSchema#string">
                       <AttributeValue>Peter</AttributeValue>
                   </Attribute>  
               </Subject>
               
               <Resource>
                   <Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" DataType="http://www.w3.org/2001/XMLSchema#string">
                       <AttributeValue>https://153.55.55.120:2354/ngsi-ld/v1/entities/urn:ngsi-ld:Sensor:humidity.201</AttributeValue>
                   </Attribute>
               </Resource> 

               <Action>
                   <Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:action:action-id" DataType="http://www.w3.org/2001/XMLSchema#string">
                       <AttributeValue>GET</AttributeValue>
                   </Attribute>  
               </Action>

               <Environment/>
            </Request>'

   **Example response**:

   .. sourcecode:: http

      <Response>
        <Result ResourceID="https://153.55.55.120:2354/ngsi-ld/v1/entities/urn:ngsi-ld:Sensor:humidity.201">
          <Decision>Permit</Decision>
          <Status>
            <StatusCode Value="urn:oasis:names:tc:xacml:1.0:status:ok"/>
          </Status>
          <Obligations>
            <Obligation ObligationId="liveTime" FulfillOn="Permit">
            </Obligation>
          </Obligations>
        </Result>
      </Response>

   :statuscode 200: no error - Permit, NotApplicable or Deny.

Test XACML - PDP is running
+++++++++++++++++++++++++++

.. http:get:: /

   Test XACML - PDP is running.

   **Example request**:

   .. tabs::

      .. code-tab:: bash
 
         $ curl --location --request GET 'https://{{XACML-PDP-IP}}:{{{XACML-PDP-Port}}/XACMLServletPDP'

   **Example response**:

   :statuscode 200: Component is running.