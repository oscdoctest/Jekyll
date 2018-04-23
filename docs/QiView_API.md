QiView API
==========

The REST APIs provide programmatic access to read and write Qi data. The APIs in this section interact 
with QiViews. When working in .NET convenient Qi Client libraries are available. The IQiMetadataService 
interface, accessed using the ``QiService.GetMetadataService()`` helper, defines the available functions. 
See `Qi View information <https://qi-docs.readthedocs.io/en/latest/QiView_information.html>`__ for general QiView information.

***********************

``Get View``
--------------

Returns the view corresponding to the specified viewId within a given namespace.


**Request**

::

    GET api/Tenants/{tenantId}/Namespaces/{namespaceId}/Views/{viewId}


**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string viewId``
  The view identifier


**Response**

  The response includes a status code and a response body.
  

**Response body**

  The requested QiView.

  Sample response body:

::
  
  HTTP/1.1 200
  Content-Type: application/json

  {  
     "Id":"View",
     "Name":"View",
     "SourceTypeId":"Simple",
     "TargetTypeId":"Simple3",
     "Properties":[  
        {  
           "SourceId":"Time",
           "TargetId":"Time"
        },
        {  
           "SourceId":"Status",
           "TargetId":"Status"
        },
        {  
           "SourceId":"Measurement",
           "TargetId":"Value"
        }
     ]
  }



**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************

``Get View Map``
--------------

Returns the view map corresponding to the specified viewId within a given namespace.


**Request**

::

    GET api/Tenants/{tenantId}/Namespaces/{namespaceId}/Views/{viewId}/Map


**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string viewId``
  The view identifier


**Response**

  The response includes a status code and a response body.
  

**Response body**

  The requested QiView.

  Sample response body:

::
  
  HTTP/1.1 200
  Content-Type: application/json

  {  
     "SourceTypeId":"Simple",
     "TargetTypeId":"Simple3",
     "Properties":[  
        {  
           "SourceId":"Time",
           "TargetId":"Time"
        },
        {  
           "SourceId":"Measurement",
           "TargetId":"Value",
           "Mode":20
        },
        {  
           "SourceId":"State",
           "Mode":2
        },
        {  
           "TargetId":"State",
           "Mode":1 
        }
     ]
  }



**.NET Library**

::

  Task<QiViewMap> GetViewMapAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************

``Get Views``
--------------

Returns a list of views within a given namespace.


**Request**

::

    GET api/Tenants/{tenantId}/Namespaces/{namespaceId}/Views?skip={skip}&count={count}


**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``int skip``
  An optional value representing the zero-based offset of the first QiView to retrieve. 
  If not specified, a default value of 0 is used.
``int count``  
  An optional value representing the maximum number of QiViews to retrieve. If not specified, 
  a default value of 100 is used.

**Response**

  The response includes a status code and a response body.
  

**Response body**

  A collection of zero or more QiViews.


**.NET Library**

::

  Task<IEnumerable<QiView>> GetViewsAsync(int skip = 0, int count = 100);
  

**Security**

  Allowed for administrator and user accounts


***********************

``Get or Create View``
--------------

If a view with a matching identifier already exists, the view passed in is compared with the existing view.
If the views are identical, the view is returned. If the views are different, the Found (302) error is returned.

If no matching identifier is found, the specified view is created.  

**Request**

::

    POST api/Tenants/{tenantId}/Namespaces/{namespaceId}/Views/{viewId}


**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string viewId``
  The view identifier. The identifier must match the ``QiView.Id`` field. 

The request content is the serialized QiView. If you are not using the Qi client libraries, using JSON is recommended.

**Response**

  The response includes a status code and a response body.
  

**Response body**

 The newly created or matching QiView.
 

**.NET Library**

::

  Task<QiView> GetOrCreateViewAsync(QiView qiView);


**Security**

  Allowed for administrator accounts


***********************

``Create or Update View``
--------------

Creates or updates the definition of a view. 

**Request**

::

    PUT api/Tenants/{tenantId}/Namespaces/{namespaceId}/Views/{viewId}


**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string viewId``
  The view identifier


**Response**

  The response includes a status code and a response body.
  

**Response body**

  The content is set to true on success.
  

**.NET Library**

::

  Task CreateOrUpdateViewAsync(QiView qiView);


**Security**

  Allowed for administrator accounts



***********************

``Delete View``
--------------

Deletes a view from the specified tenant and namespace.


**Request**

::

    GET	api/Tenants/{tenantId}/Namespaces/{namespaceId}/Views/{viewId}


**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string viewId``
  The view identifier


**Response**

  The response includes a status code.
  

**.NET Library**

::

  Task DeleteViewAsync(string viewId);

**Security**

  Allowed for administrator accounts


