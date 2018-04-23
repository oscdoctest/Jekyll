Qi Scripts
==========

You use the API calls in this section create, delete, and manage scripts.


``GetOrCreateScriptAsync()``
----------------------

Inserts the script into the specified namespaceId, or creates the script if it does not already exist. If the script exists, it is returned to the caller unchanged.  The script can be used by calculations. 

**Syntax**

.. highlight:: none

::

    Task DeletePeriodicScheduleAsync(string scheduleId);

**Http**

::

    DELETE /qi/{tenantId}/{namespaceId}/Schedules/Periodic/{scheduleId}


**Parameters**

``string Id``
  Unique Id for this script. Used when referencing this script in other objects such as calculation types or other scripts.
 
``string name``
  A Name for this script.

``string Description`` (optional)
  A Discription of this script.

``string Source``
  The source code or implementation that represents the script.

``string Type``
  The language used to write the sript = ['JavaScript', 'TypeScript']

``Array[QiScriptReference] ReferencedScripts`` (optional)
  Scripts that must be included when compiling and running this script.
 

Security
  Allowed by administrator and user accounts.

**Returns** 

::

  QiScript {Id (string): Unique Id for this script. Used when referencing this script in other objects such as calculation types or other scripts.
  Name (string): A Name for this script.
  Description (string, optional): A Discription of this script.
  Source (string): The source code or implementation that represents the script.
  Type (string): The language used to write the sript.
  = ['JavaScript', 'TypeScript']
  ReferencedScripts (Array[QiScriptReference], optional): Scripts that must be included when compiling and running this script.
  }
  QiScriptReference {
  ScriptId (string): The unique Id of the {OSIsoft.Qi.Calculation.Core.QiScript}
} 

  
  
**Status code**

*  201 - The object was added successfully.
*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

**********************



``GetScriptAsync()``
----------------------

Retrieves a script from the namespace with the specified Id.  


**Syntax**

.. highlight:: none

::

    Task<QiScript> GetScriptAsync(string scriptId);

**Http**

::

    GET /qi/{tenantId}/{namespaceId}/Scripts/{scriptId}


**Parameters**

``string Id``
  Unique Id for this script. Used when referencing this script in other objects such as calculation types or other scripts.
 
``string name``
  A Name for this script.

``string Description`` (optional)
  A Discription of this script.

``string Source``
  The source code or implementation that represents the script.

``string Type``
  The language used to write the sript = ['JavaScript', 'TypeScript']

``Array[QiScriptReference] ReferencedScripts`` (optional)
  Scripts that must be included when compiling and running this script.
 

Security
  Allowed by administrator and user accounts.

**Returns** 

::


  
**Status code**

*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

**********************

``GetScriptsAsync()``
----------------------


Retrieves a list of scripts from the specified namespace. 


**Syntax**

.. highlight:: none

::

    Task<QiScript> GetScriptsAsync(string scriptId);

**Http**

::

    GET /qi/{tenantId}/{namespaceId}/Scripts


**Parameters**

``string Id``
  Unique Id for this script. Used when referencing this script in other objects such as calculation types or other scripts.
 
``string name``
  A Name for this script.

``string Description`` (optional)
  A Discription of this script.

``string Source``
  The source code or implementation that represents the script.

``string Type``
  The language used to write the sript = ['JavaScript', 'TypeScript']

``Array[QiScriptReference] ReferencedScripts`` (optional)
  Scripts that must be included when compiling and running this script.
 

Security
  Allowed by administrator and user accounts.

**Returns** 

::


  
**Status code**

*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

**********************

``UpdateScriptAsync()``
----------------------

Updates a script in the specified namespace. 


**Syntax**

.. highlight:: none

::

    Task UpdateScriptAsync(QiScript script);

**Http**

::

    PUT /qi/{tenantId}/{namespaceId}/Scripts


**Parameters**

``string Id``
  Unique Id for this script. Used when referencing this script in other objects such as calculation types or other scripts.
 
``string name``
  A Name for this script.

``string Description`` (optional)
  A Discription of this script.

``string Source``
  The source code or implementation that represents the script.

``string Type``
  The language used to write the sript = ['JavaScript', 'TypeScript']

``Array[QiScriptReference] ReferencedScripts`` (optional)
  Scripts that must be included when compiling and running this script.
 

Security
  Allowed by administrator and user accounts.

**Returns** 

::

  QiScript {Id (string): Unique Id for this script. Used when referencing this script in other objects such as calculation types or other scripts.
  Name (string): A Name for this script.
  Description (string, optional): A Discription of this script.
  Source (string): The source code or implementation that represents the script.
  Type (string): The language used to write the sript.
  = ['JavaScript', 'TypeScript']
  ReferencedScripts (Array[QiScriptReference], optional): Scripts that must be included when compiling and running this script.
  }
  QiScriptReference {
  ScriptId (string): The unique Id of the {OSIsoft.Qi.Calculation.Core.QiScript}
} 

  
  
**Status code**

*  200 - The object was successfully updated.
*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.



**********************


 
``DeleteScriptAsync()``
----------------------


Removes a script from the specified namespace. 


**Syntax**

.. highlight:: none

::

    Task DeleteScriptAsync(string scriptId);

**Http**

::

    DELETE /qi/{tenantId}/{namespaceId}/Scripts/{scriptId}


**Parameters**

``string Id``
  Unique Id for this script. Used when referencing this script in other objects such as calculation types or other scripts.
 

Security
  Allowed by administrator and user accounts.

**Returns** 

::


  
  
**Status code**

*  200 - The object was successfully deleted.
*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 
 



