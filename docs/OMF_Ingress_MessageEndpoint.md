OMF API
=======

Because OMF messages contain all of the information needed to process them, there is a single 
endpoing for ingestion of OMF data into OSIsoft Cloud Services. 

Additional calls are available for OMF message body validation. These help determine whether 
an OMF message is compliant with the OMF specification. Any error encountered is returned in 
the response body. Note that sending a poorly crafted OMF message to the ingestion endpoint
will result in a good response indicating that it was successfully received by OCS. Parsing
of the message is performed asynchronously and any error is logged.

***************************

``POST api/omf``
-------------------------------------

Post an OMF message.

**Headers**
  OMF headers.
  
**Body**
  OMF message body encoded using UTF-8 character encoding. If compressed, the corresponding
  OMF compression header must be present.

******************************

``POST api/tenants/{tenantId}/omfvalidation/type``
-------------------------------------

Validates the body of an OMF Type message.

Parameters: 

``tenantId``
  Unique Id for the tenant. 

**Body**
  OMF Type message body in string format.

**Returns**

  A string respose for the validation result. 
  
******************************

``POST api/tenants/{tenantId}/omfvalidation/container``
-------------------------------------

Validates the body of an OMF Container message.

Parameters: 

``tenantId``
  Unique Id for the tenant. 

**Body**
  OMF Container message body in string format.

**Returns**

  A string respose for the validation result. 
  
******************************

``POST api/tenants/{tenantId}/omfvalidation/data``
-------------------------------------

Validates the body of an OMF Data message.

Parameters: 

``tenantId``
  Unique Id for the tenant. 

**Body**
  OMF Data message body in string format.

**Returns**

  A string respose for the validation result. 
  
******************************
