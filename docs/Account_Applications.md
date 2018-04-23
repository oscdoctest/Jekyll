Applications
=======================================================



``CreateClientApiKeyForApplication()``
--------------------------------------------------------------------

Create a :ref:`ClientApiKeySet <ClientApiKeySetObj>` for the specified application.

**Http**

::

	POST api/Tenants/{tenantId}/ClientApiKeySets/Keys

**Parameters**

``String tenantId``
	ID of the tenant the application belongs to.
``String applicationId``
	ID of the application for this request
``String description``
	Description of the :ref:`ClientApiKeySet <ClientApiKeySetObj>`

**Security**
	Allowed by Account Administrator :ref:`Role <RoleObj>`

**Returns**
	The created :ref:`ClientApiKeySet <ClientApiKeySetObj>`

**Notes**
	For HTTP requests and responses, the JSON serialized ClientApiKeySet object Looks like:

.. _ClientApiKeySetObj: 

.. highlight:: C#

::

 {
	"AppUri": "appuri",
	"CreateFirstKey": false,
	"DisplayName": "displayname",
	"RequiredResource":  { },
	"TenantId": "tenantid"
 }



|

**********************

``GetClientApiKeyCollectionFromApplication()``
--------------------------------------------------------------------

Get the :ref:`ClientApiKeyCollection <ClientApiKeyCollectionObj>` for the specified applicaiton.

**Http**

::

	GET api/Tenants/{tenantId}/ClientApiKeySets/Keys

**Parameters**

``String tenantId``
	ID of the tenant the application belongs to.
``String applicationId``
	ID of the application for this request

**Security**
	Allowed by Account Administrator :ref:`Role <RoleObj>`

**Returns**
	:ref:`ClientApiKeyCollection <ClientApiKeyCollectionObj>` for the specified applicaiton.

**Notes**
	For HTTP requests and responses, the JSON serialized ClientApiKeyCollection object Looks like:

.. _ClientApiKeyCollectionObj: 

.. highlight:: C#

::

 {
	"Id": "id",
	"Keys": []
 }



|

**********************

``DeleteClientApiKeyFromApplication()``
--------------------------------------------------------------------

Delete a specified :ref:`ClientApiKeySet <ClientApiKeySetObj>`.

**Http**

::

	DELETE api/Tenants/{tenantId}/ClientApiKeySets/Keys

**Parameters**

``String tenantId``
	ID of the tenant the application belongs to.
``String applicationId``
	ID of the application for this request
``String keyId``
	ID of the :ref:`ClientApiKeySet <ClientApiKeySetObj>` to be deleted.

**Security**
	Allowed by Account Administrator :ref:`Role <RoleObj>`

**Returns**
	HTTP status code - 200 OK if the :ref:`ClientApiKeySet <ClientApiKeySetObj>` was deleted.



|

**********************


