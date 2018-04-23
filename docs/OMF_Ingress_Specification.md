Using OMF with Cloud Services
=============================

The OMF specification (located `here <http://omf-docs.osisoft.com>`_) is generic in that it does
not specify a particular back-end system. This topic is a companion to the OMF specification which describes how
OMF is interpreted by OSIsoft Cloud Services back-end system. 

Headers
-------

A description of each of the headers can be found in the `OMF spec <http://omf-docs.osisoft.com>`_. When 
sending messages to OSIsoft Cloud Services, the value of the ``producertoken`` header must be 
set to a security token obtained from the OCS Portal. The security token is used to authenticate 
the sender and to authorize the sender for use with a particular Tenant and Publisher.

Message Types
-------------

OMF message types fall into three categories: Type, Container, and Data, which are described below. 

* **Type messages**

  A Type message is interpreted by OSIsoft Cloud Services as a QiType in the OCS Data Store. 
  Because QiTypes are immutable, update operations are not supported. The keywords in the 
  Type definition are interpreted as follows:
  
  + ``id``: Corresponds to the QiType Id field. It must conform to the rules defined for a 
    typeId specified `here <http://qi-docs.osisoft.com/en/latest/Qi_Types.html>`_
    
  + ``classification``: Only the ``dynamic`` classification is currently supported.
  + ``version``: Versioning of QiTypes is not supported.
  + ``name``: Corresponds to the QiType Name field. This is the friendly name for the type.
  + ``description``: Corresponds to the QIType Description field. 
  + ``tags``: Currently unsupported.
  + ``metadata``: Currently unsupported.
  
  The ``isindex`` keyword corresponds to the ``iskey`` attribute of a QiTypeProperty. 
  QiTypes support clustered indexes which can be specified with multiple properties marked 
  with the ``isindex`` keyword with a value of ``true``. For compound indexes, the 
  index property order within the message corresponds to the ``Order`` field of 
  a QiTypeProperty. The ``isname`` keyword is not supported.

* **Link Type**

  Link Types are not supported in OCS Data Store.

* **Span Type**

  Span Types are not supported in OCS Data Store.
  
* **Property Types and Formats**

  OMF supports setting the ``format`` keyword to specify how a particular JSON type should 
  be interpreted. The following is a mapping for the OCS Data Store supported 
  types (see `QiType information <http://qi-docs.osisoft.com/en/latest/Qi_Types.html>`_)


========  ===========  ============
Type      Format       QiTypeCode
========  ===========  ============
array		               IEnumerable
boolean		             boolean
integer	  int64        Int64
integer   int32        Int32
integer   int16        Int16
integer   uint64       Uint64
integer   uint32       Uint32
number    uint16       Uint16
number    float64      Double
number    float32      Single
number    float16      Single
object    dictionary   Idictionary
string                 String
string    date-time    DateTime
========  ===========  ============

  
Container messages
------------------

A Container message is interpreted as a QiStream in the OCS Data Store. The keywords 
in the Container definition are interpreted as follows:

* ``id``: Corresponds to the QiStream Id field. It must conform to the rules defined for 
  a QiStream.Id specified `here <http://qi-docs.osisoft.com/en/latest/Qi_Streams.html>`_)
* ``typeid``: Corresponds to the QiStream TypeId field.
* ``typeversion``: Versioning of QiTypes is not supported.
* ``name``: Corresponds to the QiStream Name field. This is a friendly name for the stream.
* ``description``: Corresponds to the QiStream Description field.
* ``tags``: Corresponds to the QiStream Tag field. 
* ``metadata``: Corresponds to the QiStream Metadata field        


Data messages
-------------

A Data message is mapped to generic Qi values in the OCS Data Store. The keywords in the 
Data definitions are interpreted as follows:

* ``typeid``: Data that is not grouped by containerId is not supported.
* ``containerid``: Stream Id for the associated Qi Stream.
* ``typeversion``: Not supported.
* ``values``: An array of the generic Qi values.




