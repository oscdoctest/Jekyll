Qi Calculation types
==========

The APIs in this topic are used to create, delete, and update Qi calculation types



``GetOrCreateTypeAsync()``
----------------------

Retrieves the QiCalculationType within the specified namespaceId, or creates the QiCalculationType if it does not already exist. If the QiCalculationType exists, it is returned to the caller unchanged.


**Syntax**

.. highlight:: none

::

    Task<QiCalculationType> GetOrCreateTypeAsync(QiCalculationType type);

**Http**

::

    POST /qi/{tenantId}/{namespaceId}/CalculationTypes


**Parameters**

``string Id`` (optional)
  
 
``string Name`` (optional)
  

``string Description`` (optional)
  
``QiScriptReference Script``  (optional)


``Array[QiScriptSymbol] Symbols``  (optional)
  

``string Trigger``(optional) = ['Undefined', 'PeriodicSchedule', 'EventTriggeredSchedule', 'Manual']

  
  ::

  QiScriptReference {
    ScriptId (string): The unique Id of the {OSIsoft.Qi.Calculation.Core.QiScript}
 
  }
  QiScriptSymbol {
    Id (string),
    Name (string, optional),
    ProviderId (string)
  } 
 



Security
  Allowed by administrator and user accounts.

**Returns** 


  
**Status code**

*  201 - The object was added successfully
*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

**********************

``GetTypeAsync()``
----------------------

Retrieves a QiCalculationType from a namespace. 


**Syntax**

.. highlight:: none

::

    Task<QiCalculationType> GetTypeAsync(string typeId);

**Http**

::

   GET /qi/{tenantId}/{namespaceId}/CalculationTypes/{typeId}


**Parameters**

``string Id`` (optional)
  
 
``string Name`` (optional)
  

``string Description`` (optional)
  

``QiScriptReference Script`` (optional)
  
``string Symbols`` (optional)
  
``string Trigger``(optional) = ['Undefined', 'PeriodicSchedule', 'EventTriggeredSchedule', 'Manual']

::

  QiScriptReference {
    ScriptId (string): The unique Id of the {OSIsoft.Qi.Calculation.Core.QiScript}
 
  }
  QiScriptSymbol {
    Id (string),
    Name (string, optional),
    ProviderId (string)
  } 


Security
  Allowed by administrator and user accounts.

**Returns** 


  
**Status code**

*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

**********************

``GetTypesAsync()``
----------------------

Retrieves a QiCalculationType from a namespace. 


**Syntax**

.. highlight:: none

::

    Task<IList<QiCalculationType>> GetTypesAsync();

**Http**

::

   GET /qi/{tenantId}/{namespaceId}/CalculationTypes


**Parameters**

``string Id`` (optional)
 
``string Name`` (optional)
 
``string Description`` (optional)
 
``QiScriptReference Script`` (optional)
  
``string Symbols`` (optional)
  
``string Trigger``(optional) = ['Undefined', 'PeriodicSchedule', 'EventTriggeredSchedule', 'Manual']

::

  QiScriptReference {
    ScriptId (string): The unique Id of the {OSIsoft.Qi.Calculation.Core.QiScript}
 
  }
  QiScriptSymbol {
    Id (string),
    Name (string, optional),
    ProviderId (string)
  } 


Security
  Allowed by administrator and user accounts.

**Returns** 


  
**Status code**

*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

**********************





``UpdateTypeAsync()``
----------------------

Updates an existing QiCalculationType in a namespace. 


**Syntax**

.. highlight:: none

::

    Task UpdateTypeAsync(QiCalculationType type);

**Http**

::

   PUT /qi/{tenantId}/{namespaceId}/CalculationTypes


**Parameters**

``string Id``
  
 
``string name`` (optional)
  

``string Description`` (optional)
  

``string TypeId``
  

``string ScheduleId``
  
  
``Array [QiSymbolSettings] SymbolSettings`` (optional)
  
  ::

  QiSymbolSettings {
    SymbolId (string, optional),
    ProviderSettings (object, optional)
  } 
  
  
``boolean IsEnabled``

``string Status`` = ['Undefined', 'InDevelopment', 'Running', 'InError']



Security
  Allowed by administrator and user accounts.

**Returns** 


  
**Status code**

*  200 - The object was successfully updated.
*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

**********************


``DeleteTypeAsync()``
----------------------

Removes a QiCalculationType from a namespace. 


**Syntax**

.. highlight:: none

::

    Task DeleteTypeAsync(string typeId);

**Http**

::

    DELETE /qi/{tenantId}/{namespaceId}/CalculationTypes/{typeId}


**Parameters**

``string Id``
  
 
``string name`` (optional)
  

``string Description`` (optional)
  

``string TypeId``
  

``string ScheduleId``
  
  
``Array [QiSymbolSettings] SymbolSettings`` (optional)
  
  ::

  QiSymbolSettings {
    SymbolId (string, optional),
    ProviderSettings (object, optional)
  } 
  
  
``boolean IsEnabled``

``string Status`` = ['Undefined', 'InDevelopment', 'Running', 'InError']



Security
  Allowed by administrator and user accounts.

**Returns** 


  
**Status code**

*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

**********************

