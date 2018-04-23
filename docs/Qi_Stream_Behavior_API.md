QiStreamBehavior API
====================

The REST APIs provide programmatic access to create and manipulate QiStreamBehaviors. 
The APIs in this section interact with QiStreamBehavior. When working in .NET convenient 
Qi Client libraries are available. The IQiMetadataService interface, accessed using the 
``QiService.GetMetadataService()`` helper defines the available functions. 

See `QiStreamBehavior <https://qi-docs-rst.readthedocs.org/en/latest/Qi_Stream_Behavior.html>`__ for 
general QiStreamBehavior information.


***********************


``Get Behavior``
----------------

Returns a QiStreamBehavior corresponding to the specified behaviorId.

**Request**

::

    GET api/Tenants/{tenantId}/Namespaces/{namespaceId}/Behaviors/{behaviorId}

**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string behaviorId``
  The stream behavior identifier


**Response**

The response includes a status code and a response body.

  Response body:
    The requested QiStreamBehavior
    
::

  Sample response body
  HTTP/1.1 200
  Content-Type: application/json

  {  
     "Id":"Behavior",
     "Name":"Behavior",
     "Mode":1,
     "ExtrapolationMode":1
  }

**.NET Library**

::

  Task<QiStreamBehavior> GetBehaviorAsync(string behaviorId);

**Security**

  Allowed for administrator and user accounts


**********************

``Get Behaviors``
----------------

Returns a list of stream behaviors.

**Request**

::

    GET	api/Tenants/{tenantId}/Namespaces/{namespaceId}/Behaviors
      ?skip={skip}&count={count}

**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``int skip``
  An optional parameter representing the zero-based offset of the first QiStreamBehavior to retrieve. 
  If not specified, a default value of 0 is used.
``int count``
  An optional parameter representing the maximum number of QiStreamBehaviors to retrieve. If not 
  specified, a default value of 100 is used.


**Response**

The response includes a status code and a response body.

  Response body:
    A collection of zero or more QiStreamBehaviors.
    
::

  Sample response body
  HTTP/1.1 200
  Content-Type: application/json

  [  
    {  
       "Id":"Behavior",
       "Name":"Behavior",
       "Mode":1,
       "ExtrapolationMode":1
    },
    ...
  ]


**.NET Library**

::

  Task<IEnumerable<QiStreamBehavior>> GetBehaviorsAsync(int skip = 0, 
    int count = 100);

**Security**

  Allowed for administrator and user accounts


**********************

``Get Behavior Reference Count``
------------------------------

Returns the count of streams referencing the specified behavior. 

**Request**

::

    GET	api/Tenants/{tenantId}/Namespaces/{namespaceId}/Behaviors/{behaviorId}
      /ReferenceCount


**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``String behaviorId``
  The behavior identifier


**Response**

The response includes a status code and a response body.

  Response body:
    Number of streams referencing the behavior.
    
::

  Sample response body
  HTTP/1.1 200
  Content-Type: application/json



**.NET Library**

::

  Task<int> GetBehaviorReferenceCountAsync(string behaviorId); 

**Security**

  Allowed for administrator and user accounts


**********************

``Create Behavior``
------------------

Creates the specified stream behavior. If a stream behavior with a matching identifier already exists, Qi compares the 
existing stream behavior with the stream behavior that was sent. If the stream behaviors are identical, a ``Found`` (302) error 
is returned with the Location header set to the URI where the stream behavior may be retrieved using a Get function. 
If the stream behaviors do not match, a ``Conflict`` (409) error is returned.

For a matching stream behavior (Found), clients that are capable of performing a redirect that includes the 
authorization header can automatically redirect to retrieve the stream behavior. However, most clients, 
including the .NET HttpClient, consider redirecting with the authorization token to be a security vulnerability.

When a client performs a redirect and strips the authorization header, Qi cannot authorize the request and 
returns ``Unauthorized`` (401). For this reason, it is recommended that when using clients that do not 
redirect with the authorization header, you should disable automatic redirect.



**Request**

::

    POST api/Tenants/{tenantId}/Namespaces/{namespaceId}/Behaviors/{behaviorId}
    
**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string behaviorId``
  The stream behavior identifier. The behavior identifier must match the identifier in content.

The request content is the serialized QiStreamBehavior. If you are not using the Qi client libraries, 
OSIsoft recommends using JSON.

Sample QiStreamBehavior content:

::

  {  
     "Id":"Behavior",
     "Name":"Behavior",
     "Mode":1,
     "ExtrapolationMode":1,
     "Overrides":[  
        {  
           "QiTypePropertyId":"Measurement",
           "Mode":0
        }
     ]
  }



**Response**

The response includes a status code and a response body.

  Response body:
    The newly created QiStreamBehavior.
    

**.NET Library**

``Task<QiStreamBehavior> GetOrCreateBehaviorAsync(QiStreamBehavior qiBehavior);``

  If a behavior with a matching identifier already exists and it matches the behavior in the request body, 
  the client redirects a GET to the Location header. If the existing behavior does not match the behavior 
  in the request body, a Conflict error response is returned and the client library method throws an exception. 


The following sample shows how to create a stream behavior with a Mode of StepwiseContinuousLeading, 
no extrapolation and an override of a Property.

::

  QiStreamBehavior behavior = new QiStreamBehavior()
  {
      Id = "Behavior",
      Name = "Behavior",
      Mode = QiStreamMode.StepwiseContinuousLeading,
      ExtrapolationMode = QiStreamExtrapolation.None,
      Overrides = new List<QiStreamBehaviorOverride>
      {
          new QiStreamBehaviorOverride()
          {
              QiTypePropertyId = "Measurement",
              Mode = QiStreamMode.Continuous
          }
      }
  };
  behavior = await config.CreateBehaviorAsync(behavior);


**Security**

  Allowed for administrator accounts


*********************


``Create or Update Behavior``
---------------------------

Creates the specified behavior. If a behavior with the same Id already exists, the definition 
of the behavior is updated.

**Request**

::

    PUT	api/Tenants/{tenantId}/Namespaces/{namespaceId}/Behaviors/{behaviorId}
    
**Parameters**

``string tenantId``
  The tenant identifier of the tenant where you want to update the stream
``string namespaceId``
  The namespace identifier of the namespace where you want to update the stream
``string behaviorId``
  The stream behavior identifier to be updated
  
The request content is the serialized QiStreamBehavior.  
  

**Response**

The response includes a status code.


**.NET Library**

::

 Task CreateOrUpdateBehaviorAsync(QiStreamBehavior qiBehavior);



**Security**

  Allowed for administrator accounts


********************

``Delete Behavior``
----------------

Deletes a stream behavior. You cannot delete a stream behavior that is associated with a stream.

**Request**

::

   DELETE api/Tenants/{tenantId}/Namespaces/{namespaceId}/Behaviors/{behaviorId}
   
**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string behaviorId``
  The stream behavior identifier


**Response**

The response includes a status code.


**.NET Library**

::

  Task DeleteBehaviorAsync(string behaviorId);
  
**Security**

  Allowed for administrator accounts








