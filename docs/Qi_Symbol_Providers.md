QiSymbolProviders
=================


``GetSymbolProviders()``
----------------------

Returns a list of supported QiSymbolProvider objects. Symbol providers are used to map variables in scripts to different data source providers such as Qi and Azure Event Hubs. 


**Syntax**

.. highlight:: none

::

    Task<IList<QiSymbolProvider>> GetSymbolProviders();

**Http**

::

    GET /qi/SymbolProviders


**Parameters**

``string Description`` (optional)
  
  
``string Id`` (optional)
  
``string Name`` (optional)

``Array[QiProviderSetting] Settings`` (optional) (read only)

::

  QiProviderSetting {
    Id (string),
    Description (string),
    Type (string) = ['Empty', 'Object', 'DBNull', 'Boolean', 'Char', 'SByte', 'Byte', 'Int16', 'UInt16', 'Int32', 'UInt32', 'Int64', 'UInt64', 'Single', 'Double', 'Decimal', 'DateTime', 'String', 'Guid', 'DateTimeOffset', 'TimeSpan', 'Version', 'NullableBoolean', 'NullableChar', 'NullableSByte', 'NullableByte', 'NullableInt16', 'NullableUInt16', 'NullableInt32', 'NullableUInt32', 'NullableInt64', 'NullableUInt64', 'NullableSingle', 'NullableDouble', 'NullableDecimal', 'NullableDateTime', 'NullableGuid', 'NullableDateTimeOffset', 'NullableTimeSpan', 'BooleanArray', 'CharArray', 'SByteArray', 'ByteArray', 'Int16Array', 'UInt16Array', 'Int32Array', 'UInt32Array', 'Int64Array', 'UInt64Array', 'SingleArray', 'DoubleArray', 'DecimalArray', 'DateTimeArray', 'StringArray', 'GuidArray', 'DateTimeOffsetArray', 'TimeSpanArray', 'VersionArray', 'Array', 'IList', 'IDictionary', 'IEnumerable', 'QiType', 'QiTypeProperty', 'SByteEnum', 'ByteEnum', 'Int16Enum', 'UInt16Enum', 'Int32Enum', 'UInt32Enum', 'Int64Enum', 'UInt64Enum', 'NullableSByteEnum', 'NullableByteEnum', 'NullableInt16Enum', 'NullableUInt16Enum', 'NullableInt32Enum', 'NullableUInt32Enum', 'NullableInt64Enum', 'NullableUInt64Enum']
    IsRequired (boolean)
  }


Security
  Allowed by administrator and user accounts.

**Returns** 
  Returns a namespace.
  
**Status code**


 

**********************
