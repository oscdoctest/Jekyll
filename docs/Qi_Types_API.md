QiType API
==========

The REST APIs provide programmatic access to read and write Qi data. The APIs in this section 
interact with QiTypes. When working in .NET convenient Qi Client libraries are available. 
The IQiMetadataService interface, accessed using theQiService.GetMetadataService( ) helper, 
defines the available functions. See
`Qi Types <https://qi-docs.readthedocs.io/en/latest/Qi_Types.html>`__.
for general QiType information.


***********************

``Get Type``
------------

Returns the type corresponding to the specified typeId within a given namespace.

**Request**

::

    GET api/Tenants/{tenantId}/Namespaces/{namespaceId}/Types/{typeId}


**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string typeId``
  The type identifier


**Response**

The response includes a status code and a response body.

**Response body**

  The requested QiType
  
  Sample response body:
  
::

  HTTP/1.1 200
  Content-Type: application/json

  {  
     "Id":"f1a7ef61-d47f-3007-a260-449643a7c219",
     "Name":"Simple",
     "QiTypeCode":1,
     "Properties":[  
        {  
           "Id":"Time",
           "Name":"Time",
           "IsKey":true,
           "QiType":{  
              "$id":"567",
              "Id":"19a87a76-614a-385b-ba48-6f8b30ff6ab2",
              "Name":"DateTime",
              "QiTypeCode":16
           }
        },
        {  
           "Id":"State",
          "Name":"State",
           "QiType":{  
              "$id":"569",
              "Id":"e20bdd7e-590b-3372-ab39-ff61950fb4f3",
              "Name":"State",
              "QiTypeCode":609,
              "Properties":[  
                 {  
                    "$id":"570",
                    "Id":"Ok",
                    "Value":0
                 },
                 {  
                    "$id":"571",
                    "Id":"Warning",
                    "Value":1
                 },
                 {  
                    "$id":"572",
                    "Id":"Aalrm",
                    "Value":2
                 }
              ]
           }
        },
        {  
           "$id":"573",
           "Id":"Measurement",
           "Name":"Measurement",
           "QiType":{  
              "$id":"574",
              "Id":"6fecef77-20b1-37ae-aa3b-e6bb838d5a86",
              "Name":"Double",
              "QiTypeCode":14
           }
        }
     ]
  }



**.NET Library**

::

  Task<QiType> GetTypeAsync(string typeId);


**Security**

  Allowed by administrator and user accounts


***********************

``Get Types``
------------

Returns a list of types within a given namespace.

**Request**

::

    GET api/Tenants/{tenantId}/Namespaces/{namespaceId}/Types?skip={skip}&count={count}


**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``int skip``
  An optional value representing the zero-based offset of the first QiType to retrieve. If not specified, a default value of 0 is used.
``int count``
  An optional value representing the maximum number of QiTypes to retrieve. If not specified, a default value of 100 is used.

**Response**

  The response includes a status code and a response body.

**Response body**

  A collection of zero or more QiTypes.
  
  Sample response body:
  
::

  HTTP/1.1 200
  Content-Type: application/json

  [  
    {  
        "Id":"f1a7ef61-d47f-3007-a260-449643a7c219",
        "Name":"Simple",
        "QiTypeCode":1,
        "Properties":[  
           {  
              "Id":"Time",
              "Name":"Time",
              "IsKey":true,
              "QiType":{  
                 "Id":"19a87a76-614a-385b-ba48-6f8b30ff6ab2",
                 "Name":"DateTime",
                 "QiTypeCode":16
              }
           },
           {  
              "Id":"State",
              "Name":"State",
              "QiType":{  
                 "Id":"e20bdd7e-590b-3372-ab39-ff61950fb4f3",
                 "Name":"State",
                 "QiTypeCode":609,
                 "Properties":[  
                    {  
                       "Id":"Ok",
                       "Value":0
                    },
                    {  
                       "Id":"Warning",
                       "Value":1
                    },
                    {  
                       "Id":"Aalrm",
                       "Value":2
                    }
                 ]
              }
           },
           {  
              "Id":"Measurement",
              "Name":"Measurement",
              "QiType":{  
                 "$id":"574",
                 "Id":"6fecef77-20b1-37ae-aa3b-e6bb838d5a86",
                 "Name":"Double",
                 "QiTypeCode":14
              }
           }
        ]
     },
     …
  ]



**.NET Library**

::

  Task<IEnumerable<QiType>> GetTypesAsync(int skip = 0, int count = 100);


**Security**

  Allowed by administrator and user accounts


***********************

``Create Type``
-------------

Creates the specified type. If a type with a matching identifier already exists, Qi compares the 
existing type with the type that was sent. If the types are identical, a ``Found`` (302) error 
is returned with the Location header set to the URI where the type may be retrieved using a Get function. 
If the types do not match, a ``Conflict`` (409) error is returned.

For a matching type (``Found``), clients that are capable of performing a redirect that includes the 
authorization header can automatically redirect to retrieve the type. However, most clients, 
including the .NET HttpClient, consider redirecting with the authorization token to be a security vulnerability.

When a client performs a redirect and strips the authorization header, Qi cannot authorize the request and 
returns ``Unauthorized`` (401). For this reason, it is recommended that when using clients that do not 
redirect with the authorization header, you should disable automatic redirect.


**Request**

::

    POST api/Tenants/{tenantId}/Namespaces/{namespaceId}/Types/{typeId}

**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string typeId``
  The type identifier. The identifier must match the QiType.Id field. 


**Response**

  The response includes a status code and a response body.

**Response body**

  The request content is the serialized QiType. If you are not using the Qi client libraries, we recommend using JSON.
  
  Sample QiType content:
  
::

  {  
     "Id":"Simple",
     "Name":"Simple",
     "Description":"Basic sample type",
     "QiTypeCode":1,
     "IsGenericType":false,
     "IsReferenceType":false,
     "GenericArguments":null,
     "Properties":[  
        {  
           "Id":"Time",
           "Name":"Time",
           "Description":null,
           "Order":0,
           "IsKey":true,
           "FixedSize":0,
           "QiType":{  
              "Id":"c48bfdf5-a271-384b-bf13-bd21d931c1bf",
              "Name":"DateTime",
              "Description":null,
              "QiTypeCode":16,
              "IsGenericType":false,
              "IsReferenceType":false,
              "GenericArguments":null,
              "Properties":null,
              "BaseType":null,
              "DerivedTypes":null
           },
           "Value":null
        },
        {  
           "Id":"State",
           "Name":"State",
           "Description":null,
           "Order":0,
           "IsKey":false,
           "FixedSize":0,
           "QiType":{  
              "Id":"ba5d20e1-cd21-3ad0-99f3-c3a3b0146aa1",
              "Name":"State",
              "Description":null,
              "QiTypeCode":609,
              "IsGenericType":false,
              "IsReferenceType":false,
              "GenericArguments":null,
              "Properties":[  
                 {  
                    "Id":"Ok",
                    "Name":null,
                    "Description":null,
                    "Order":0,
                    "IsKey":false,
                    "FixedSize":0,
                    "QiType":null,
                    "Value":0
                 },
                 {  
                    "Id":"Warning",
                    "Name":null,
                    "Description":null,
                    "Order":0,
                    "IsKey":false,
                    "FixedSize":0,
                    "QiType":null,
                    "Value":1
                 },
                 {  
                    "Id":"Alarm",
                    "Name":null,
                    "Description":null,
                    "Order":0,
                    "IsKey":false,
                    "FixedSize":0,
                    "QiType":null,
                    "Value":2
                 }
              ],
              "BaseType":null,
              "DerivedTypes":null
           },
           "Value":null
        },
        {  
           "Id":"Measurement",
           "Name":"Measurement",
           "Description":null,
           "Order":0,
           "IsKey":false,
           "FixedSize":0,
           "QiType":{  
              "Id":"0f4f147f-4369-3388-8e4b-71e20c96f9ad",
              "Name":"Double",
              "Description":null,
              "QiTypeCode":14,
              "IsGenericType":false,
              "IsReferenceType":false,
              "GenericArguments":null,
              "Properties":null,
              "BaseType":null,
              "DerivedTypes":null
           },
           "Value":null
        }
     ],
     "BaseType":null,
     "DerivedTypes":null
  }


Response

The response includes a status code and a response body.
  
Response body
  
::

  HTTP/1.1 200
  Content-Type: application/json

  {  
     "Id":"Simple",
     "Name":"Simple",
     "Description":"Basic sample type",
     "QiTypeCode":1,
     "Properties":[  
        {  
           "Id":"Time",
           "Name":"Time",
           "IsKey":true,
           "QiType":{  
              "$id":"596",
              "Id":"c48bfdf5-a271-384b-bf13-bd21d931c1bf",
              "Name":"DateTime",
              "QiTypeCode":16
           }
        },
        {  
           "Id":"State",
           "Name":"State",
           "QiType":{  
              "$id":"598",
              "Id":"ba5d20e1-cd21-3ad0-99f3-c3a3b0146aa1",
              "Name":"State",
              "QiTypeCode":609,
              "Properties":[  
                 {  
                    "Id":"Ok",
                    "Value":0
                 },
                 {  
                    "Id":"Warning",
                    "Value":1
                 },
                 {  
                    "Id":"Alarm",
                    "Value":2
                 }
              ]
           }
        },
        {  
           "Id":"Measurement",
           "Name":"Measurement",
           "QiType":{  
              "Id":"0f4f147f-4369-3388-8e4b-71e20c96f9ad",
              "Name":"Double",
              "QiTypeCode":14
           }
        }
     ]
  }
  



**.NET Library**

 
  ``Task<QiType> GetOrCreateTypeAsync(QiType qiType);``

  If a type with a matching identifier already exists and it matches the type in the request body, 
  the client redirects a GET to the Location header. If the existing type does not match the type
  in the request body, a Conflict error response is returned and the client library method throws an exception. 

  The Qi .NET Libraries manage redirects.

**Security**

  Allowed by administrator accounts


***********************



``Create or Update Type``
------------------------

Creates the specified type. If a type with the same Id already exists, the definition of the type is updated.

Note that a type cannot be updated if any streams are 
associated with it. Also, certain parameters, including the type id, cannot be changed after 
they are defined.

**Request**

::

    PUT api/Tenants/{tenantId}/Namespaces/{namespaceId}/Types/{typeId}


**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string typeId``
  The type identifier


**Response**

  The response includes a status code and a response body.

**Response body**

  The content is set to true on success.
  

**.NET Library**

::
 
  Task CreateOrUpdateTypeAsync(QiType qiType)


**Security**

  Allowed by administrator accounts


***********************



``Delete Type``
------------

Deletes a type from the specified tenant and namespace. Note that a type cannot be deleted if any streams reference it.

**Request**

::

    DELETE	api/Tenants/{tenantId}/Namespaces/{namespaceId}/Types/{typeId}
    

**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string typeId``
  The type identifier


**Response**

  The response includes a status code.


**.NET Library**

::

  Task DeleteTypeAsync(string typeId);


**Security**

  Allowed by administrator accounts


