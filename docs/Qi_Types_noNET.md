Working with QiTypes when not using .NET
----------------------------------------


QiTypes must be built manually when .NET QiTypeBuilder is unavailable. The following discussion 
refers to the types that are defined in  
`Python <https://github.com/osisoft/Qi-Samples/tree/master/Basic/Python>`__ and 
`JavaScript <https://github.com/osisoft/Qi-Samples/tree/master/Basic/JavaScript>`__ samples. 
Samples in other languages can be found here: `Samples <https://github.com/osisoft/Qi-Samples/tree/master/Basic>`__.

In the sample code, ``QiType``, ``QiTypeProperty``, and ``QiTypeCode`` are defined as in the code snippets shown here:

**Python**

::

  class QiTypeCode(Enum):
      Empty = 0
      Object = 1
      DBNull = 2
      Boolean = 3
      Char = 4
        ...
  class QiTypeProperty(object):
      """Qi type property definition"""

      def __init__(self):
              self.__isKey = False

      @property
      def Id(self):
          return self.__id
      @Id.setter
      def Id(self, id):
          self.__id = id

        ...

      @property
      def IsKey(self):
          return self.__isKey
      @IsKey.setter
      def IsKey(self, iskey):
          self.__isKey = iskey

      @property
      def QiType(self):
          return self.__qiType
      @QiType.setter
      def QiType(self, qiType):
          self.__qiType=qiType
        ...

  class QiType(object):
      """Qi type definitions"""
      def __init__(self):
          self.QiTypeCode = QiTypeCode.Object

      @property
      def Id(self):
          return self.__id
      @Id.setter
      def Id(self, id):
          self.__id = id

        ...

      @property
      def BaseType(self):
          return self.__baseType
      @BaseType.setter
      def BaseType(self, baseType):
          self.__baseType = baseType

      @property
      def QiTypeCode(self):
          return self.__typeCode
      @QiTypeCode.setter
      def QiTypeCode(self, typeCode):
          self.__typeCode = typeCode

      @property
      def Properties(self):
          return self.__properties
      @Properties.setter
      def Properties(self, properties):
          self.__properties = properties

 
  
**JavaScript**

::

  qiTypeCodeMap: {
      Empty: 0,
      "Object": 1,
      DBNull: 2,
      "Boolean": 3,
      Char: 4,
      ...
  QiTypeProperty: function (qiTypeProperty) {
      if (qiTypeProperty.Id) {
          this.Id = qiTypeProperty.Id;
      }
      if (qiTypeProperty.Name) {
          this.Name = qiTypeProperty.Name;
      }
      if (qiTypeProperty.Description) {
          this.Description = qiTypeProperty.Description;
      }
      if (qiTypeProperty.QiType) {
          this.QiType = qiTypeProperty.QiType;
      }
      if (qiTypeProperty.IsKey) {
          this.IsKey = qiTypeProperty.IsKey;
      }
  },
  QiType: function (qiType) {
      if (qiType.Id) {
          this.Id = qiType.Id
      }
      if (qiType.Name) {
          this.Name = qiType.Name;
      }
      if (qiType.Description) {
          this.Description = qiType.Description;
      }
      if (qiType.QiTypeCode) {
          this.QiTypeCode = qiType.QiTypeCode;
      }
      if (qiType.Properties) {
          this.Properties = qiType.Properties;
      }
  },



Working with the following types (both Python and JavaScript classes are shown):


**Python**

::

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

      Measurement = property(getMeasurement, setMeasurement)
      def getMeasurement(self):
          return self.__measurement
      def setMeasurement(self, measurement):
          self.__measurement = measurement


**JavaScript**

::

  var State =
    {
        Ok: 0,
        Warning: 1,
        Aalrm: 2,
    }
 
    var Simple = function () {
        this.Time = null;
        this.State = null;
        this.Measurement = null;
    }

 
Define the QiType as follows:

**Python**

::

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
  stateTypePropertyOk.Value = State.Ok
  stateTypePropertyWarning = QiTypeProperty()
  stateTypePropertyWarning.Id = "Warning"
  stateTypePropertyWarning.Value = State.Warning
  stateTypePropertyAlarm = QiTypeProperty()
  stateTypePropertyAlarm.Id = "Alarm"
  stateTypePropertyAlarm.Value = State.Alarm

  stateType = QiType()
  stateType.Id = "State"
  stateType.Name = "State"
  stateType.Properties = [ stateTypePropertyOk, stateTypePropertyWarning, \
                          stateTypePropertyAlarm ]

  state = QiTypeProperty()
  state.Id = "State"
  state.Name = "State"
  state.QiType = stateType

  # Value property is a simple non-indexed, pre-defined type
  value = QiTypeProperty()
  value.Id = "Measurement"
  value.Name = "Measurement"
  value.QiType = QiType()
  value.QiType.Id = "Double"
  value.QiType.Name = "Double"

  # Create the Simple QiType
  simpleType = QiType()
  simpleType.Id = "Simple"
  simpleType.Name = "Simple"
  simpleType.Description = "Basic sample type"
  simpleType.QiTypeCode = QiTypeCode.Object
  simpleType.Properties = [ time ]


**JavaScript**

::

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

  // Measurement property is a simple non-indexed, pre-defined type
  var measurementProperty = new QiObjects.QiTypeProperty({
      "Id": "Measurement",
      "Name": "Measurement",
      "QiType": new QiObjects.QiType({
          "Id": "doubleType",
          "QiTypeCode": QiObjects.qiTypeCodeMap.Double
      })
  });

  // Create the Simple QiType
  var simpleType = new QiObjects.QiType({
      "Id": "Simple",
      "Name": "Simple", 
      "Description": " This is a simple Qi type ",
      "QiTypeCode": QiObjects.qiTypeCodeMap.Object,
      "Properties": [timeProperty, stateProperty, measurementProperty]
  });


 Working with a derived class is easy. For the following derived class:

::

  class Derrived(Simple):
      @property
      def Observation(self):
          return self.__observation
      @Observation.setter
      def Observation(self, observation):
          self.__observation = observation


Extend the QiType as follows:

**Python**

::

  # Observation property is a simple non-inexed, standard data type
  observation = QiTypeProperty()
  observation.Id = "Observation"
  observation.Name = "Observation"
  observation.QiType = QiType()
  observation.QiType.Id = "String"
  observation.QiType.Name = "String"
  observation.QiType.QiTypeCode = QiTypeCode.String

  # Create the Derived QiType
  derived = QiType()
  derived.Id = "Derived"
  derived.Name = "Derived"
  derived.Description = "Derived sample type"
  derived.BaseType = simpleType # Set the base type to the derived type
  derived.QiTypeCode = QiTypeCode.Object
  derived.Properties = [ observation ]
    

**JavaScript**

::

  var observationProprety = new QiObjects.QiTypeProperty({
      "Id": "Observation",
      "QiType": new QiObjects.QiType({
          "Id": "strType",
          "QiTypeCode": QiObjects.qiTypeCodeMap.String
      })
  });

  var derivedType = new QiObjects.QiType({
      "Id": "Derived",
      "Name": "Derived",
      "Description": " Derived sample type",
      "BaseType": simpleType,
      "QiTypeCode": QiObjects.qiTypeCodeMap.Object,
      "Properties": [ observationProprety ]
  });
