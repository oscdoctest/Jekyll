﻿Qi Indexes topic

=======
Indexes
=======

Indexes speed up and order the results of searches. A key uniquely identifies a record within 
a collection of records. Keys are unique within the collection.

In Qi, the key of a QiType is also an index. The key is often referred to as the *primary index,* 
while all other indexes are referred to as *secondary indexes* or *secondaries*.

A QiType that is used to define a QiStream must specify a key. When inserting data into a QiStream, every 
key value must be unique. Qi will not store more than a single event for a given key; an event with 
a particular key may be deleted or updated, but two events with the same key cannot exist.

In .NET, the QiType properties that define the key are identified using an ``OSIsoft.Qi.QiMemberAttribute`` 
and setting its ``IsKey`` field to true. If the key consists of only a single property it is permissible to 
use the ``System.ComponentModel.DataAnnotations.KeyAttribute``. In the QiType, the Property or Properties 
representing the key have their ``QiTypeProperty.IsKey`` field set to true.

Secondary indexes are defined on QiStreams and are applied to a single property. You can define many 
secondary indexes. Secondary index values need not be unique.



Compound Indexes
----------------

Often, a single property (such as a DateTime), is adequate for defining an index; however, for more complex 
scenarios, Qi allows you to define multiple properties. Indexes defined by multiple properties are known as *compound indexes*.

When defining a compound index in .NET, you should apply the ``OSIsoft.Qi.QiMemberAttribute`` on each of the type’s 
properties that are combined to define the index. Set the ``IsKey`` property to ``true`` and give ``Orderfield`` a 
zero-based index value. The ``Order`` field defines the precedence of the property when sorting. A property with 
an order of 0 has highest precedence.

When defining compound indexes outside of .NET, specify the ``IsKey`` and ``Order`` fields on the ``QiTypePropertyor``
Properties.

Only the primary index (or key) supports compound indexes.

You can specify a maximum of three Properties to define a compound index.

The Qi REST API methods that use tuples were created to assist you when using compound indexes.


Working with Indexes
--------------------

Using .NET
----------


Simple Indexes
--------------

When working in .NET, use the QiTypeBuilder together with either the ``OSIsoft.Qi.QiMemberAttribute`` or the
``System.ComponentModel.DataAnnotations.KeyAttribute`` to identify the Property that defines the simple Key. 
The ``QiMemberAttribute`` is preferred. Using QiTypeBuilder eliminates potential errors that might occur 
when working with QiTypes manually.


::

  public enum State
  {
    Ok,
    Warning,
    Alarm
  }

  public class Simple
  {
    [QiMember(IsKey = true, Order = 0) ]
    public DateTime Time { get; set; }
    public State State { get; set; }
    public Double Measurement { get; set; }
  }

  QiType simpleType = QiTypeBuilder.CreateQiType<Simple>();


To read data that is located between two indexes, ordered by the Key, define both a start index and 
an end index. For DateTime, use ISO 8601 representation of dates and times. For example, to query 
for a window of simple values between January 1, 2010 and February 1, 2010, you can define indexes 
and query as follows.

::

  IEnumerable<Simple> values = await
  client.GetWindowValuesAsync<Simple>(simpleStream.Id,
  "2010-01-01T08:00:00.000Z","2010-02-01T08:00:00.000Z");


More information about querying data can be found in `Reading Data <https://qi-docs.readthedocs.org/en/latest/Reading_Data.html>`__.


**Secondary Indexes**

Secondary indexes are defined at the QiStream. To add indexes to a QiStream, you add them to the QiStream’s Indexes field.

For example, to add a second index on Measurement, use the following code:


::

  QiStreamIndex measurementIndex = new QiStreamIndex()
  {
      QiTypePropertyId = simpleType.Properties.First(p => p.Id.Equals("Measurement")).Id
  };
  QiStream secondary = new QiStream()
  {
      Id = "Simple with Secondary",
      TypeId = simpleType.Id,
      Indexes = new List<QiStreamIndex>()
      {
          measurementIndex
      }
  };
  secondary = await config.GetOrCreateStreamAsync(secondary);


To read data indexed by a secondary Index, use a filtered Get, as in the following:

::

  await client.UpdateValuesAsync<Simple>(secondary.Id, new List<Simple>()
    {
        new Simple()
        {
            Time = time,
            State = State.Ok,
            Measurement = 5
        },
        new Simple()
        {
            Time = time + TimeSpan.FromSeconds(1),
            State = State.Ok,
            Measurement = 4
        },
        new Simple()
        {
            Time = time + TimeSpan.FromSeconds(2),
            State = State.Ok,
            Measurement = 3
        },
        new Simple()
        {
            Time  = time + TimeSpan.FromSeconds(3),
            State = State.Ok,
            Measurement = 2
        },
        new Simple()
        {
            Time = time + TimeSpan.FromSeconds(4),
            State = State.Ok,
            Measurement = 1
        },
    });

  IEnumerable<Simple> orderedByKey = await client.GetWindowValuesAsync<Simple>(secondary.Id, 
      time.ToString("o"), time.AddSeconds(4).ToString("o"));
  foreach (Simple value in orderedByKey)
      Console.WriteLine("{0}: {1}", value.Time, value.Measurement);

  Console.WriteLine();

  IEnumerable<Simple> orderedBySecondary = await client.GetFilteredValuesAsync<Simple>(secondary.Id, 
  "Measurement gt 0 and Measurement lt 6");
  foreach (Simple value in orderedBySecondary)
      Console.WriteLine("{0}: {1}", value.Time, value.Measurement);
  Console.WriteLine();

  // Output:
  // 1/20/2017 12:00:00 AM: 5
  // 1/20/2017 12:00:01 AM: 4
  // 1/20/2017 12:00:02 AM: 3
  // 1/20/2017 12:00:03 AM: 2
  // 1/20/2017 12:00:04 AM: 1
  //
  // 1/20/2017 12:00:04 PM: 1
  // 1/20/2017 12:00:03 PM: 2
  // 1/20/2017 12:00:02 PM: 3
  // 1/20/2017 12:00:01 PM: 4
  // 1/20/2017 12:00:00 PM: 5

  
  
Compound Indexes
----------------

Compound indexes are defined using the QiMemberAttribute as follows:

::

  public class Simple
  {
    [QiMember(IsKey = true, Order = 0)]
    public DateTime Time { get; set; }
    public State State { get; set; }
    public Double Measurement { get; set; }
  }

  public class DerivedCompoundIndex : Simple
  {
    [QiMember(IsKey = true, Order = 1)]
    public DateTime Recorded { get; set; } 
  }


Events of type DerivedCompoundIndex are sorted first by the Time parameter and then by the Recorded parameter. A collection of times would be sorted as follows:


+------------+----------------+-------------------+
| **Time**   | **Recorded**   | **Measurement**   |
+============+================+===================+
| 01:00      | 00:00          | 0                 |
+------------+----------------+-------------------+
| 01:00      | 01:00          | 2                 |
+------------+----------------+-------------------+
| 01:00      | 14:00          | 5                 |
+------------+----------------+-------------------+
| 02:00      | 00:00          | 1                 |
+------------+----------------+-------------------+
| 02:00      | 01:00          | 3                 |
+------------+----------------+-------------------+
| 02:00      | 02:00          | 4                 |
+------------+----------------+-------------------+
| 02:00      | 14:00          | 6                 |
+------------+----------------+-------------------+

If the Order parameters were swapped, Recorded set to zero, and Time set to one, the results would sort as follows:

+------------+----------------+-------------------+
| **Time**   | **Recorded**   | **Measurement**   |
+============+================+===================+
| 01:00      | 00:00          | 0                 |
+------------+----------------+-------------------+
| 02:00      | 00:00          | 1                 |
+------------+----------------+-------------------+
| 01:00      | 01:00          | 2                 |
+------------+----------------+-------------------+
| 02:00      | 01:00          | 3                 |
+------------+----------------+-------------------+
| 02:00      | 02:00          | 4                 |
+------------+----------------+-------------------+
| 01:00      | 14:00          | 5                 |
+------------+----------------+-------------------+
| 02:00      | 14:00          | 6                 |
+------------+----------------+-------------------+


::

  // estimates at 1/20/2017 00:00
  await client.UpdateValuesAsync(compoundStream.Id, new List<DerivedCompoundIndex>()
    {
        new DerivedCompoundIndex()
        {
            Time = DateTime.Parse("1/20/2017 01:00"),
            Recorded = DateTime.Parse("1/20/2017 00:00"),
            State = State.Ok,
            Measurement = 0
        },
        new DerivedCompoundIndex()
        {
            Time = DateTime.Parse("1/20/2017 02:00"),
            Recorded = DateTime.Parse("1/20/2017 00:00"),
            State = State.Ok,
            Measurement = 1
        },
    });

  // measure and estimates at 1/20/2017 01:00
  await client.UpdateValuesAsync(compoundStream.Id, new List<DerivedCompoundIndex>()
    {
        new DerivedCompoundIndex()
        {
            Time = DateTime.Parse("1/20/2017 01:00"),
            Recorded = DateTime.Parse("1/20/2017 01:00"),
            State = State.Ok,
            Measurement = 2
        },
        new DerivedCompoundIndex()
        {
            Time = DateTime.Parse("1/20/2017 02:00"),
            Recorded = DateTime.Parse("1/20/2017 01:00"),
            State = State.Ok,
            Measurement = 3
        },
    });

  // measure at 1/20/2017 02:00
  await client.UpdateValuesAsync(compoundStream.Id, new List<DerivedCompoundIndex>()
    {
        new DerivedCompoundIndex()
        {
            Time = DateTime.Parse("1/20/2017 02:00"),
            Recorded = DateTime.Parse("1/20/2017 02:00"),
            State = State.Ok,
            Measurement = 4
        },
    });

  // adjust earlier values at 1/20/2017 14:00
  await client.UpdateValuesAsync(compoundStream.Id, new List<DerivedCompoundIndex>()
    {
        new DerivedCompoundIndex()
        {
            Time = DateTime.Parse("1/20/2017 01:00"),
            Recorded = DateTime.Parse("1/20/2017 14:00"),
            State = State.Ok,
            Measurement = 5
        },
        new DerivedCompoundIndex()
        {
            Time = DateTime.Parse("1/20/2017 02:00"),
            Recorded = DateTime.Parse("1/20/2017 14:00"),
            State = State.Ok,
            Measurement = 6
        },
    });

  var from = new Tuple<DateTime, DateTime>(DateTime.Parse("1/20/2017 01:00"), DateTime.Parse("1/20/2017 00:00"));
  var to = new Tuple<DateTime, DateTime>(DateTime.Parse("1/20/2017 02:00"), DateTime.Parse("1/20/2017 14:00"));

  var compoundValues = await client.GetWindowValuesAsync<DerivedCompoundIndex, DateTime, DateTime>(compoundStream.Id, from, to);

  foreach (DerivedCompoundIndex value in compoundValues)
     Console.WriteLine("{0}:{1} {2}", value.Time, value.Recorded, value.Measurement);

  // Output:
  // 1/20/2017 1:00:00 AM:1/20/2017 12:00:00 AM 0
  // 1/20/2017 1:00:00 AM:1/20/2017 1:00:00 AM 2
  // 1/20/2017 1:00:00 AM:1/20/2017 2:00:00 PM 5
  // 1/20/2017 2:00:00 AM:1/20/2017 12:00:00 AM 1
  // 1/20/2017 2:00:00 AM:1/20/2017 1:00:00 AM 3
  // 1/20/2017 2:00:00 AM:1/20/2017 2:00:00 AM 4
  // 1/20/2017 2:00:00 AM:1/20/2017 2:00:00 PM 6

Note that the ``GetWindowValuesAsync()`` call specifies an expected return type and the index types as generic parameters.


Not Using .NET
--------------


Simple Indexes
--------------


When the .NET QiTypeBuilder is unavailable, indexes must be built manually.


The following discusses the types defined in the `Python <https://github.com/osisoft/Qi-Samples/tree/master/Basic/Python>`__
and `Java Script <https://github.com/osisoft/Qi-Samples/tree/master/Basic/JavaScript>`__
samples. Samples in other languages can be found `here <https://github.com/osisoft/Qi-Samples/tree/master/Basic>`__.

To build a QiType representation of the following sample class, see code_example_1_:

*Python*

.. code-block:: python

  class State(Enum):
    Ok = 0
    Warning = 1
    Alarm = 2

  class Simple(object):
    Time = property(getTime, setTime)
    def getTime(self):
      return self.__time
    def setTime(self, time):
      self.__time = time

    State = property(getState, setState)
    def getState(self):
      return self.__state
    def setState(self, state):
      self.__state = state

    Measurement = property(getValue, setValue)
    def getValue(self):
      return self.__measurement
    def setValue(self, measurement):
      self.__measurement = measurement


*JavaScript*

.. code-block:: javascript

  var State =
  {
    Ok: 0,
    Warning: 1,
    Aalrm: 2,
  }

  var Simple = function () {
    this.Time = null;
    this.State = null;
    this.Value = null;
  }

.. _code_example_1:

The following code is used to build a QiType representation of the sample class above:

*Python*

.. code-block:: python

  # Create the properties

  # Time is the primary key
  time = QiTypeProperty()
  time.Id = "Time"
  time.Name = "Time"
  time.IsKey = True
  time.QiType = QiType()
  time.QiType.Id = "DateTime"
  time.QiType.Name = "DateTime"
  time.QiType.QiTypeCode = QiTypeCode.DateTime

  # State is not a pre-defined type. A QiType must be defined to represent the enum
  stateTypePropertyOk = QiTypeProperty()
  stateTypePropertyOk.Id = "Ok"
  stateTypePropertyOk.Measurement = State.Ok
  stateTypePropertyWarning = QiTypeProperty()
  stateTypePropertyWarning.Id = "Warning"
  stateTypePropertyWarning.Measurement = State.Warning
  stateTypePropertyAlarm = QiTypeProperty()
  stateTypePropertyAlarm.Id = "Alarm"
  stateTypePropertyAlarm.Measurement = State.Alarm

  stateType = QiType()
  stateType.Id = "State"
  stateType.Name = "State"
  stateType.Properties = [ stateTypePropertyOk, stateTypePropertyWarning,\
                         stateTypePropertyAlarm ]
  state = QiTypeProperty()
  state.Id = "State"
  state.Name = "State"
  state.QiType = stateType

  # Measurement property is a simple non-indexed, pre-defined type
  measurement = QiTypeProperty()
  measurement.Id = "Measurement"
  measurement.Name = "Measurement"
  measurement.QiType = QiType()
  measurement.QiType.Id = "Double"
  measurement.QiType.Name = "Double"

  # Create the Simple QiType
  simple = QiType()
  simple.Id = str(uuid.uuid4())
  simple.Name = "Simple"
  simple.Description = "Basic sample type"
  simple.QiTypeCode = QiTypeCode.Object
  simple.Properties = [ time, state, measurement ]


*JavaScript*

.. code-block:: javascript

  // Time is the primary key
  var timeProperty = new QiObjects.QiTypeProperty({
    "Id": "Time",
    "IsKey": true,
    "QiType": new QiObjects.QiType({
      "Id": "dateType",
      "QiTypeCode": QiObjects.qiTypeCodeMap.DateTime
    })
  });

  // State is not a pre-defined type. A QiType must be defined to represent the enum
  var stateTypePropertyOk = new QiObjects.QiTypeProperty({
    "Id": "Ok",
    "Value": State.Ok
  });

  var stateTypePropertyWarning = new QiObjects.QiTypeProperty({
    "Id": "Warning",
    "Value": State.Warning
  });

  var stateTypePropertyAlarm = new QiObjects.QiTypeProperty({
    "Id": "Alarm",
    "Value": State.Alarm
  });

  var stateType = new QiObjects.QiType({
    "Id": "State",
    "Name": "State",
    "QiTypeCode": QiObjects.qiTypeCodeMap.Int32Enum,
    "Properties": [stateTypePropertyOk, stateTypePropertyWarning,
      stateTypePropertyAlarm, stateTypePropertyRed]
  });

  // Value property is a simple non-indexed, pre-defined type
  var valueProperty = new QiObjects.QiTypeProperty({
    "Id": "Value",
    "QiType": new QiObjects.QiType({
      "Id": "doubleType",
      "QiTypeCode": QiObjects.qiTypeCodeMap.Double
    })
  });

  // Create the Simple QiType
  var simpleType = new QiObjects.QiType({
    "Id": "Simple",
    "Name": "Simple",
    "Description": "This is a simple Qi type",
    "QiTypeCode": QiObjects.qiTypeCodeMap.Object,
    "Properties": [timeProperty, stateProperty, valueProperty]
  });


The Time property is identified as the Key by define its QiTypeProperty as follows:

*Python*

.. code-block:: python

  # Time is the primary key
  time = QiTypeProperty()
  time.Id = "Time"
  time.Name = "Time"
  time.IsKey = True
  time.QiType = QiType()
  time.QiType.Id = "DateTime"
  time.QiType.Name = "DateTime"
  time.QiType.QiTypeCode = QiTypeCode.DateTime

*JavaScript*

.. code-block:: javascript

  // Time is the primary key
  var timeProperty = new QiObjects.QiTypeProperty({
    "Id": "Time",
    "IsKey": true,
    "QiType": new QiObjects.QiType({
      "Id": "dateType",
      "QiTypeCode": QiObjects.qiTypeCodeMap.DateTime
    })
  });



Note that the time.IsKey field is set to true.

To read data using the key, you define a start index and an end index. For DateTime, use 
ISO 8601 representation of dates and times. To query for a window of values between January 1, 
2010 and February 1, 2010, you would define indexes as “2010-01-01T08:00:00.000Z” and 
“2010-02-01T08:00:00.000Z”, respectively.

Additional information can be found in the `Reading Data <https://qi-docs.readthedocs.org/en/latest/Reading_Data.html>`__.

**Secondary Indexes**

Secondary Indexes are defined at the QiStream. To create a QiStream 
using the Simple class and add a Secondary index on the Measurement, 
you use the previously defined QiType. Then you create a QiStreamIndex 
specifying the measurement property and define a QiStream identifying the 
Measurement as a Secondary Index as shown in the following example:


*Python*

.. code-block:: python

  # Create the properties

  measurementIndex = QiStreamIndex()
  measurementIndex.QiTypePropertyId = measurement.Id

  stream = QiStream()
  stream.Id = str(uuid.uuid4())
  stream.Name = "SimpleWithSecond"
  stream.Description = "Simple with secondary index"
  stream.TypeId = simple.Id
  stream.Indexes = [ measurementIndex ]



*JavaScript*

.. code-block:: javascript

  var measurementIndex = new QiObjects.QiStreamIndex({
    "QiTypePropertyId": valueProperty.Id
  });

  var stream = new QiObjects.QiStream({
    "Id": "SimpleWithSecond",
    "Name": "SimpleWithSecond",
    "Description": "Simple with secondary index",
    "TypeId": simpleTypeId,
    "Indexes": [ measurementIndex ]
  });


Compound Indexes
----------------

Consider the following Python and JavaScript types:

*Python*

.. code-block:: python

  class Simple(object):
  # First-order Key property
  Time = property(getTime, setTime)
  def getTime(self):
    return self.__time
  def setTime(self, time):
    self.__time = time

  State = property(getState, setState)
  def getState(self):
    return self.__state
  def setState(self, state):
    self.__state = state

  Measurement = property(getValue, setValue)
  def getValue(self):
    return self.__measurement
  def setValue(self, measurement):
    self.__measurement = measurement

  class DerivedCompoundIndex(Simple):
  # Second-order Key property
  @property
  def Recorded(self):
    return self.__recorded
  @Recorded.setter
  def Recorded(self, recorded):
    self.__recorded = recorded


*JavaScript*

.. code-block:: javascript

  var Simple = function () {
    this.Time = null;
    this.State = null;
    this.Value = null;
  }

  var DerivedCompoundIndex = function() {
    Simple.call(this);
    this.Recorded = null;
  }


To turn the simple QiType shown in the example into a type supporting the DerivedCompoundIndex 
type with a compound index based on the ``Simple.Time`` and ``DerivedCompoundIndex.Recorded``, 
extend the type as follows:

*Python*

.. code-block:: python

  # We set the Order for this property. The order of the first property defaulted to 0
  recorded = QiTypeProperty()
  recorded.Id = "Recorded"
  recorded.Name = "Recorded"
  recorded.IsKey = True
  recorded.Order = 1
  recorded.QiType = QiType()
  recorded.QiType.Id = "DateTime"
  recorded.QiType.Name = "DateTime"
  recorded.QiType.QiTypeCode = QiTypeCode.DateTime

  # Create the Derived QiType
  derived = QiType()
  derived.Id = str(uuid.uuid4())
  derived.Name = "Compound"
  derived.Description = "Derived compound index sample type"
  derived.BaseType = simple
  derived.QiTypeCode = QiTypeCode.Object
  derived.Properties = [ recorded ]



*JavaScript*

.. code-block:: javascript

  // We set the Order for this property. The order of the first property defaulted to 0
  var recordedProperty = new QiObjects.QiTypeProperty({
    "Id": "Recorded",
    "Name": "Recorded",
    "IsKey": true,
    "Order": 1,
    "QiType": new QiObjects.QiType({
      "Id": "DateTime",
      "Name": "DateTime",
      "QiTypeCode": QiObjects.qiTypeCodeMap.DateTime
    })
  });

  // Create the Derived QiType
  var derivedType = new QiObjects.QiTyp({
    "Id": "Compound",
    "Name": "Compound",
    "Description": "Derived compound index sample type",
    "BaseType": simpleType,
    "QiTypeCode": QiObjects.qiTypeCodeMap.Object,
    "Properties": [recordedProperty]
  });

 
Data in the stream will be ordered as follows:

+------------+----------------+-------------------+
| **Time**   | **Recorded**   | **Measurement**   |
+============+================+===================+
| 01:00      | 00:00          | 0                 |
+------------+----------------+-------------------+
| 01:00      | 01:00          | 2                 |
+------------+----------------+-------------------+
| 01:00      | 14:00          | 5                 |
+------------+----------------+-------------------+
| 02:00      | 00:00          | 1                 |
+------------+----------------+-------------------+
| 02:00      | 01:00          | 3                 |
+------------+----------------+-------------------+
| 02:00      | 02:00          | 4                 |
+------------+----------------+-------------------+
| 02:00      | 14:00          | 6                 |
+------------+----------------+-------------------+

If the Order was swapped, and Recorded set as zero, the results would sort as
follows:

+------------+----------------+-------------------+
| **Time**   | **Recorded**   | **Measurement**   |
+============+================+===================+
| 01:00      | 00:00          | 0                 |
+------------+----------------+-------------------+
| 02:00      | 00:00          | 1                 |
+------------+----------------+-------------------+
| 01:00      | 01:00          | 2                 |
+------------+----------------+-------------------+
| 02:00      | 01:00          | 3                 |
+------------+----------------+-------------------+
| 02:00      | 02:00          | 4                 |
+------------+----------------+-------------------+
| 01:00      | 14:00          | 5                 |
+------------+----------------+-------------------+
| 02:00      | 14:00          | 6                 |
+------------+----------------+-------------------+



