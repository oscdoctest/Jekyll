.. _Qi_Stream_behavior_topic:

Qi Stream Behaviors
===================

Qi stores collections of events and provides convenient ways to find and associating events. 
Events of consistent structure are stored in streams, called QiStreams. The stream’s behavior 
when attempting to read non-existent indexes, indexes that fall between, before or after existing 
indexes, is determined by the QiStreamBehavior. 

For an index that falls between existing data events, QiStreamBehavior can specify that Qi return 
an interpolated value or the value from the preceding event. Similarly, if the read index occurs 
before or after all of the stream’s data, the stream behavior determines whether extrapolation is 
applied. 

A *QiStreamBehavior* is defined on the QiStream. Even if no behavior is assigned to a stream, it 
behaves in a default manner.

QiStreamBehavior management using the Qi Client Libraries is performed through the IQiMetadataService, 
using one of the QiService.GetMetadataService( ) factory methods.

The StreamBehavior object consists of the following properties:


+------------------+--------------------------------+------------+---------------------------------------------------+
|Property          |Type                            |Optionality | Details                                           |
+==================+================================+============+===================================================+
|Id                |String                          |Required    | Uniquely identifies the behavior                  |
+------------------+--------------------------------+------------+---------------------------------------------------+
|Name              |String                          |Optional    | Friendly name                                     |
+------------------+--------------------------------+------------+---------------------------------------------------+
|Mode              |QiStreamMode                    |Optional    | Interpolation setting. Default is Continuous      |
+------------------+--------------------------------+------------+---------------------------------------------------+
|ExtrapolationMode |QiStreamExtrapolation           |Optional    | Extrapolation setting. Default is All             |
+------------------+--------------------------------+------------+---------------------------------------------------+
|Overrides         |IList<QiStreamBehaviorOverride> |Optional    | Property level settings overriding Mode setting.  |
+------------------+--------------------------------+------------+---------------------------------------------------+

A stream’s behavior can be changed at any time and behaviors can be changed at any time, even while the stream is in use.


**Rules for QiStreamBehavior Id**

1. Not case sensitive
2. Spaces are allowed
3. Cannot start with two underscores ("\_\_")
4. Cannot contain forward slashes or backslashes ("/" or "\\")
5. Can contain a maximum of 260 characters
6. Cannot start or end with a period.
7. Cannot contain consecutive periods.
8. Cannot consist of only periods. 

**Methods affected by QiStreamBehavior**

`GetValueAsync <https://qi-docs-rst.readthedocs.org/en/latest/Reading_Data_API.html#getvalueasync>`__
  Stream behavior is applied when the index is between, before, or after all data.

`GetValuesAsync <https://qi-docs-rst.readthedocs.org/en/latest/Reading_Data_API.html#getvaluesasync>`__
  Stream behavior is applied when an index determined by the call is between, before, or after all data.

`GetWindowValuesAsync <https://qi-docs-rst.readthedocs.org/en/latest/Reading_Data_API.html#getwindowvaluesasync>`__
  Stream behavior is applied to indexes between, before, or after data when the calls Boundary parameter is set to ExactOrCalculated.

`GetRangeValuesAsync <https://qi-docs-rst.readthedocs.org/en/latest/Reading_Data_API.html#getrangevaluesasync>`__
  Stream behavior is applied to indexes between, before, or after data when the calls Boundary parameter is set to ExactOrCalculated.




Interpolation
------------

Interpolation determines how a stream behaves when asked to return an event at an index between 
two existing events. Mode determines how the returned event is constructed. The table below lists Modes:

+---------------------------+--------------------------------+--------------------------------------------------+
|Mode                       |Enumeration value               |Operation                                         |
+===========================+================================+==================================================+
|Default                    |0                               |The default Mode is Continuous                    |
+---------------------------+--------------------------------+--------------------------------------------------+
|Continuous                 |0                               |Interpolates the data using previous and next     |
|                           |                                |index values                                      |
+---------------------------+--------------------------------+--------------------------------------------------+
|StepwiseContinuousLeading  |1                               |Returns the data from the previous index          |
+---------------------------+--------------------------------+--------------------------------------------------+
|StepwiseContinuousTrailing |2                               |Returns the data from the next index              |
+---------------------------+--------------------------------+--------------------------------------------------+
|Discrete                   |3                               |Returns ‘null’                                    |
+---------------------------+--------------------------------+--------------------------------------------------+

Note that ``Continuous`` cannot return events for values that cannot be interpolated, such as when the type is not numeric.

The table below describes how the **Continuous Mode** affects
indexes that occur between data in a stream:

***Mode* = Continuous or Default**

+---------------------------+--------------------------------+--------------------------------------------------+
|Type                       |Result for an index between     |Comment                                           |
|                           |data in a stream                |                                                  |
+===========================+================================+==================================================+
|Numeric Types              |Interpolated*                   |Rounding is done as needed for integer types      |
+---------------------------+--------------------------------+--------------------------------------------------+
|Time related Types         |Interpolated                    |DateTime, DateTimeOffset, TimeSpan                |
+---------------------------+--------------------------------+--------------------------------------------------+
|Nullable Types             |Returns ‘null’                  |Cannot reliably interpolate due to possibility of |
|                           |                                |a null value                                      |
+---------------------------+--------------------------------+--------------------------------------------------+
|Array and List Types       |Returns ‘null’                  |                                                  |
+---------------------------+--------------------------------+--------------------------------------------------+
|String Type                |Returns ‘null’                  |                                                  |
+---------------------------+--------------------------------+--------------------------------------------------+
|Boolean Type               |Returns value of nearest index  |                                                  |
+---------------------------+--------------------------------+--------------------------------------------------+
|Enumeration Types          |Returns Enum value at 0         |This may have a value for the enumeration         |
+---------------------------+--------------------------------+--------------------------------------------------+
|GUID                       |                                |                                                  |
+---------------------------+--------------------------------+--------------------------------------------------+
|Version                    |Returns ‘null’                  |                                                  |
+---------------------------+--------------------------------+--------------------------------------------------+
|IDictionary or IEnumerable |Returns ‘null’                  |Dictionary, Array, List, and so on.               |
+---------------------------+--------------------------------+--------------------------------------------------+

\*When extreme values are involved in an interpolation (for example
Decimal.MaxValue) the call might result in a BadRequest exception.

Extrapolation
------------

Extrapolation defines how a stream responds to requests with indexes that precede or follow all 
data in the steam. ExtrapolationMode acts as a master switch to determine whether extrapolation 
occurs and at which end of the data. 

ExtrapolationMode works with the Mode to determine how a stream responds. The following tables 
show how ExtrapolationMode affects returned values for each Mode value:

**ExtrapolationMode with Mode\ =Default or Continuous**

+---------------------+---------------------+----------------------------+---------------------------+
| ExtrapolationMode   | Enumeration value   | Index before data          | Index after data          |
+=====================+=====================+============================+===========================+
| All                 | 0                   | Returns first data value   | Returns last data value   |
+---------------------+---------------------+----------------------------+---------------------------+
| None                | 1                   | Return null                | Return null               |
+---------------------+---------------------+----------------------------+---------------------------+
| Forward             | 2                   | Returns first data value   | Return null               |
+---------------------+---------------------+----------------------------+---------------------------+
| Backward            | 3                   | Return null                | Returns last data value   |
+---------------------+---------------------+----------------------------+---------------------------+

***ExtrapolationMode* with *Mode*\ =Discrete**

+---------------------+---------------------+---------------------+--------------------+
| ExtrapolationMode   | Enumeration value   | Index before data   | Index after data   |
+=====================+=====================+=====================+====================+
| All                 | 0                   | Return null         | Return null        |
+---------------------+---------------------+---------------------+--------------------+
| None                | 1                   | Return null         | Return null        |
+---------------------+---------------------+---------------------+--------------------+
| Forward             | 2                   | Return null         | Return null        |
+---------------------+---------------------+---------------------+--------------------+
| Backward            | 3                   | Return null         | Return null        |
+---------------------+---------------------+---------------------+--------------------+

***ExtrapolationMode* with *Mode*\ =StepwiseContinuousLeading**

+---------------------+---------------------+----------------------------+---------------------------+
| ExtrapolationMode   | Enumeration value   | Index before data          | Index after data          |
+=====================+=====================+============================+===========================+
| All                 | 0                   | Returns first data value   | Returns last data value   |
+---------------------+---------------------+----------------------------+---------------------------+
| None                | 1                   | Return null                | Return null               |
+---------------------+---------------------+----------------------------+---------------------------+
| Forward             | 2                   | Returns first data value   | Return null               |
+---------------------+---------------------+----------------------------+---------------------------+
| Backward            | 3                   | Return null                | Returns last data value   |
+---------------------+---------------------+----------------------------+---------------------------+

***ExtrapolationMode* with *Mode*\ =StepwiseContinuousTrailing**

+---------------------+---------------------+----------------------------+---------------------------+
| ExtrapolationMode   | Enumeration value   | Index before data          | Index after data          |
+=====================+=====================+============================+===========================+
| All                 | 0                   | Returns first data value   | Returns last data value   |
+---------------------+---------------------+----------------------------+---------------------------+
| None                | 1                   | Return null                | Return null               |
+---------------------+---------------------+----------------------------+---------------------------+
| Forward             | 2                   | Returns first data value   | Return null               |
+---------------------+---------------------+----------------------------+---------------------------+
| Backward            | 3                   | Return null                | Returns last data value   |
+---------------------+---------------------+----------------------------+---------------------------+

For additional information about the effect of stream behaviors, see the
documentation on the `read
method <https://qi-docs-rst.readthedocs.org/en/latest/Reading_Data_API.html>`__
you are using.

Overrides
---------

Overrides provide a way to override interpolation behavior, Mode, for individual QiType properties.

The *Override* object has the following structure:


+------------------+--------------------------------+------------+---------------------------------------------------+
|Property          |Type                            |Optionality | Details                                           |
+==================+================================+============+===================================================+
|QiTypePropertyId  |String                          |Required    | QiType Property’s identifier                      |
+------------------+--------------------------------+------------+---------------------------------------------------+
|Mode              |QiStreamMode                    |Required    | Interpolation setting. Default is Continuous      |
+------------------+--------------------------------+------------+---------------------------------------------------+

When specifying overrides, a Mode setting of Discrete cannot be overridden. When Mode is set to Discrete, 
a null value is returned for the entire event. 


.. toctree::

   Qi_Stream_Behavior_API


