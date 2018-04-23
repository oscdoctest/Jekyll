Qi Periodic Schedules
=====================

The API calls in this section are all used to create, delete, and manage periodic schedules within a namespace. Schedules can be referenced by calculations. 



``GetOrCreatePeriodicScheduleAsync()``
-------------------


Inserts a new periodic schedule into the specified namespaceId, or creates the periodic schedule if it does not already exist. If the periodic schedule exists, it is returned to the caller unchanged. The schedule can be referenced by calculations. 


**Syntax**

.. highlight:: none

::

   Task<QiPeriodicSchedule> GetOrCreatePeriodicScheduleAsync(QiPeriodicSchedule schedule);

**Http**

::

    POST /qi/{tenantId}/{namespaceId}/Schedules/Periodic


**Parameters**

``string Id``
  Unique Id for this schedule. Used when referencing this schedule or retrieving it.
``string Name``
  A name for this schedule.
``string TimeZoneId`` (optional)
  The Id of the time zone used for this schedule. Used only when the schedule uses daily, monthly, or yearly schedules.
``string ScheduleType``
  Used to determine how the time interval is expressed = ['TimeInterval', 'Daily', 'Monthly', 'Yearly']
``string Interval`` (optional)
  The interval expressed as hh:mm[:ss[.ff]] where hh is the number of hours, mm is the number of minutes, ss is the optional number of seconds, and ff is the number of fractional seconds. Used only when the ScheduleType is TimeInterval.
``string Offset`` (optional)
  An offset applied to the schedule. If a TimeInterval schedule has an Interval of 01:00, or one hour, and an offset of 00:05, then it will be dispatched at five minutes after the hour, every hour.
 
Security
  Allowed by administrator and user accounts.

**Returns** 
  Returns a namespace.

**Status code**

* 201 - Created
* 400 - BadRequest
* 500 - InternalServerError

 

**********************


``GetPeriodicScheduleAsync()``
-------------------

Retrieves a periodic schedule that is associated with a specified Id. 


**Syntax**

.. highlight:: none

::

   Task<QiPeriodicSchedule> GetPeriodicScheduleAsync(string scheduleId);

**Http**

::

    GET /qi/{tenantId}/{namespaceId}/Schedules/Periodic/{scheduleId}


**Parameters**

``string Id``
  Unique Id for this schedule. Used when referencing this schedule or retrieving it.
``string Name``
  A name for this schedule.
``string TimeZoneId`` (optional)
  The Id of the time zone used for this schedule. Used only when the schedule uses daily, monthly, or yearly schedules.
``string ScheduleType``
  Used to determine how the time interval is expressed = ['TimeInterval', 'Daily', 'Monthly', 'Yearly']
``string Interval`` (optional)
  The interval expressed as hh:mm[:ss[.ff]] where hh is the number of hours, mm is the number of minutes, ss is the optional number of seconds, and ff is the number of fractional seconds. Used only when the ScheduleType is TimeInterval.
``string Offset`` (optional)
  An offset applied to the schedule. If a TimeInterval schedule has an Interval of 01:00, or one hour, and an offset of 00:05, then it will be dispatched at five minutes after the hour, every hour.
 
Security
  Allowed by administrator and user accounts.

**Returns** 
  Returns a namespace.

**Status code**

*  200 - OK
*  404 - BadRequest
*  500 - InternalServerError


**********************

``GetPeriodicSchedulesAsync()``
-------------------

 Returns a list of periodic schedules used by calculations


**Syntax**

.. highlight:: none

::

    Task<IList<QiPeriodicSchedule>> GetPeriodicSchedulesAsync();

**Http**

::

    GET /qi/{tenantId}/{namespaceId}/Schedules/Periodic


**Parameters**

``string Id``
  Unique Id for this schedule. Used when referencing this schedule or retrieving it.
``string Name``
  A name for this schedule.
``string TimeZoneId`` (optional)
  The Id of the time zone used for this schedule. Used only when the schedule uses daily, monthly, or yearly schedules.
``string ScheduleType``
  Used to determine how the time interval is expressed = ['TimeInterval', 'Daily', 'Monthly', 'Yearly']
``string Interval`` (optional)
  The interval expressed as hh:mm[:ss[.ff]] where hh is the number of hours, mm is the number of minutes, ss is the optional number of seconds, and ff is the number of fractional seconds. Used only when the ScheduleType is TimeInterval.
``string Offset`` (optional)
  An offset applied to the schedule. If a TimeInterval schedule has an Interval of 01:00, or one hour, and an offset of 00:05, then it will be dispatched at five minutes after the hour, every hour.
 
Security
  Allowed by administrator and user accounts.

**Returns** 
  Returns a namespace.

**Status code**

* 400 - BadRequest
* 500 - InternalServerError


*************************

 

``UpdatePeriodicScheduleAsync()``
-------------------

 Updates a periodic schedule in a specified namespace. 


**Syntax**

.. highlight:: none

::

    Task UpdatePeriodicScheduleAsync(QiPeriodicSchedule schedule);

**Http**

::

   PUT /qi/{tenantId}/{namespaceId}/Schedules/Periodic


**Parameters**

``string Id``
  Unique Id for this schedule. Used when referencing this schedule or retrieving it.
``string Name``
  A name for this schedule.
``string TimeZoneId`` (optional)
  The Id of the time zone used for this schedule. Used only when the schedule uses daily, monthly, or yearly schedules.
``string ScheduleType``
  Used to determine how the time interval is expressed = ['TimeInterval', 'Daily', 'Monthly', 'Yearly']
``string Interval`` (optional)
  The interval expressed as hh:mm[:ss[.ff]] where hh is the number of hours, mm is the number of minutes, ss is the optional number of seconds, and ff is the number of fractional seconds. Used only when the ScheduleType is TimeInterval.
``string Offset`` (optional)
  An offset applied to the schedule. If a TimeInterval schedule has an Interval of 01:00, or one hour, and an offset of 00:05, then it will be dispatched at five minutes after the hour, every hour.
 
Security
  Allowed by administrator and user accounts.

**Returns** 
  Returns a namespace.

**Status code**

* 400 - BadRequest
* 500 - InternalServerError

 

**********************

``DeletePeriodicScheduleAsync()``
----------------------

Removes a periodic schedule from the specified namespace. 


**Syntax**

.. highlight:: none

::

    Task DeletePeriodicScheduleAsync(string scheduleId);

**Http**

::

    DELETE /qi/{tenantId}/{namespaceId}/Schedules/Periodic/{scheduleId}


**Parameters**

``string tenantId``
  The ID of the tenant.
  
``string NamespaceId``
  The ID of the namespace.
  
``string Id``
  The Id of the schedule.
 
Security
  Allowed by administrator and user accounts.

**Returns** 
  Returns a namespace.
  
**Status code**

*  200 - OK
*  400 - BadRequest
*  500 - InternalServerError
 

**********************


