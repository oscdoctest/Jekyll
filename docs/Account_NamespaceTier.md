NamespaceTier
=======================================================

An attribute that specifies namespace performance.

	The following code shows the JSON-serialized NamespaceTier object for HTTP requests and responses:

.. _NamespaceTierObj: 

.. highlight:: C#

::

 {
	"Id": "id",                            //GUID for this Namespace Tier.
	"Description": "description",          //Description of this Tier.
	"ThroughputUnits": 0,                  //The number of throughput units associated with this Tier.
	"StorageUnits": 0,                     //The number of Storage units associated with this Tier.
	"CalculationUnits": 0                  //The number of calculation units associated with this Tier.
 }

``GetNamespaceTier()``
--------------------------------------------------------------------

Retrieves a Namespace tier associated with a specified id

**Http**

::

	GET api/NamespaceTiers/{namespaceTierId}

**Parameters**

``String namespaceTierId``
	The tier identifier for this request

**Security**
	Allowed by Account Member :ref:`Role <RoleObj>`

**Returns**
	A :ref:`NamespaceTier <NamespaceTierObj>` object with the specified namespaceTierId



|

**********************

``GetAllNamespaceTiers()``
--------------------------------------------------------------------

Retrieves a list of all available namespace tiers.

**Http**

::

	GET api/NamespaceTiers

**Parameters**


**Security**
	Allowed by Account Member :ref:`Role <RoleObj>`

**Returns**
	An array of :ref:`NamespaceTier <NamespaceTierObj>` objects



|

**********************


