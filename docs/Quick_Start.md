.. _Quick_start_topic:

===========
Quick start
===========

.. contents:: Topics in this section:
    :depth: 3

Qi quick start
--------------

Qi is a sophisticated data store. The information in this section describes a very simple interaction with Qi.
To follow along with the steps in this section, you will first need a Tenant and associated security credentials. 
If you have not already acquired a tenant, email Qi support at: `OSIsoft Cloud Services <cloudservices@osisoft.com>`__.

The Preview is limited; contacting OSIsoft does not assure participation. 

Throughout this guide, you will be instructed to interact with the Portal. To access the section 
identified, you must sign into the Portal using the credentials associated with the Tenant.

You will also need a Namespace and administrative client keys.  See Namespace information and API Client Keys.


Step 1: Acquire a Namespace
**************************

Navigate to the OSIsoft Cloud Services page. Then, select the Manage tab and select Namespaces. For the 
steps in this section, you can use either an existing Namespace or you can create a new Namespace.


Step 2: Acquire client keys
***************************

For this example, the application acts as a confidential client – an application that is capable 
of securely maintaining a secret. In Azure Active Directory, the confidential client authentication 
flow is accomplished via an Application Identity. OSIsoft Cloud Services supports this authentication 
with Client Key and Secret.

To acquire the Client Key from the portal, select Client Keys under Manage, as shown in the following image:

.. image:: images/Acquire_Client_Key.png

You can either select an existing key or create a new key. Click the eye icon next to the desired key 
to see configuration information. You will need the Tenant Identity, Client Identity and Client Secret.  
These will be used to acquire a security Token from an identity provider, Azure Active Directory.


Step 3: Acquire authentication token
************************************

You will use the Tenant Identity, Client Identity and Client Secret to acquire an access token 
from Azure Active Directory. Click on the eye icon next to the desired key to see the values 
and code samples for various languages.

.. image:: images/Acquire_Token.png



Step 4: Create data types
*************************

A QiType describes the structure of a single measured event or object. A QiStream has an associated 
QiType and stores a stream of events or objects that take the shape of that type.

A QiType consists of one or more data properties, one of which must represent an index. Indexes can be 
simple, such as a single integer property, or compound, represented by multiple properties. 
DateTime is a common index for time-series stores. 

Qi supports a wide variety of property types, including simple types like integers, strings and floats 
and complex types like lists, arrays and enumerations. Properties can be of any complex QiType. 
For additional information, including a detailed list of supported data types, refer to :ref:`Qi_Types_topic`.

To create a  QiType in .NET, use the .NET Qi libraries QiTypeBuilder.

::

  public enum State
  {
      Ok,
      Warning,
      Alarm
  }

  public class Simple
  {
      [QiMember(IsKey = true, Order = 0)]
      public DateTime Time { get; set; }
      public State State { get; set; }
      public Double Measurement { get; set; }
  }

  QiType simpleType = QiTypeBuilder.CreateQiType<Simple>();
         simpleType.Id = "Simple";
         simpleType.Name = "Simple";
         simpleType.Description = "Basic sample type";
  await config.CreateTypeAsync(simpleType);

When working outside of .NET,  Qi libraries are unavailable. The QiType is defined using JSON and is posted to the OSIsoft Cloud Services endpoint.

::

  POST /api/Tenants/{tenantId}/Namespaces/{namespaceId}/Types/{typeId}  HTTP/1.1
  Authorization: Bearer <bearer-token>
  Content-Length: 1562
  Content-Type: application/json
  Host: dat-a.osisoft.com
  {  
     "$id":"1",
     "Id":"Simple",
     "Name":"Simple",
     "Description":"Basic sample type",
     "QiTypeCode":1,
     "IsGenericType":false,
     "IsReferenceType":false,
     "GenericArguments":null,
     "Properties":[  
        {  
           "Id":"Time",
           "Name":"Time",
           "Description":null,
           "Order":0,
           "IsKey":true,
           "FixedSize":0,
           "QiType":{  
              "$id":"2",
              "Id":"c48bfdf5-a271-384b-bf13-bd21d931c1bf",
              "Name":"DateTime",
              "Description":null,
              "QiTypeCode":16,
              "IsGenericType":false,
              "IsReferenceType":false,
              "GenericArguments":null,
              "Properties":null,
              "BaseType":null,
              "DerivedTypes":null
           },
           "Value":null
        },
        {  
           "Id":"State",
           "Name":"State",
           "Description":null,
           "Order":0,
           "IsKey":false,
           "FixedSize":0,
           "QiType":{  
              "$id":"3",
              "Id":"ba5d20e1-cd21-3ad0-99f3-c3a3b0146aa1",
              "Name":"State",
              "Description":null,
              "QiTypeCode":609,
              "IsGenericType":false,
              "IsReferenceType":false,
              "GenericArguments":null,
              "Properties":[  
                 {  
                    "Id":"Ok",
                    "Name":null,
                    "Description":null,
                    "Order":0,
                    "IsKey":false,
                    "FixedSize":0,
                    "QiType":null,
                    "Value":0
                 },
                 {  
                    "Id":"Warning",
                    "Name":null,
                    "Description":null,
                    "Order":0,
                    "IsKey":false,
                    "FixedSize":0,
                    "QiType":null,
                    "Value":1
                 },
                 {  
                    "Id":"Alarm",
                    "Name":null,
                    "Description":null,
                    "Order":0,
                    "IsKey":false,
                    "FixedSize":0,
                    "QiType":null,
                    "Value":2
                 }
              ],
              "BaseType":null,
              "DerivedTypes":null
           },
           "Value":null
        },
        {  
           "Id":"Measurement",
           "Name":"Measurement",
           "Description":null,
           "Order":0,
           "IsKey":false,
           "FixedSize":0,
           "QiType":{  
              "$id":"4",
              "Id":"0f4f147f-4369-3388-8e4b-71e20c96f9ad",
              "Name":"Double",
              "Description":null,
              "QiTypeCode":14,
              "IsGenericType":false,
              "IsReferenceType":false,
              "GenericArguments":null,
              "Properties":null,
              "BaseType":null,
              "DerivedTypes":null
           },
           "Value":null
        }
     ],
     "BaseType":null,
     "DerivedTypes":null
  }


Step 5: Create a stream
***********************

A QiStream has an associated QiType and stores a stream of events or objects that take the shape of that type. 
Detailed information about streams can be found in QiStreams.

Create a QiStream of Simple events using the .NET Qi libraries as follows:

::

  QiStream simpleStream = new QiStream() 
  {
      Id = "Simple",
      Name = "Simple",
      TypeId = simpleType.Id
  };

  simpleStream = config.CreateStreamAsync(simpleStream);

To create the stream without the libraries, post a JSON representation of the QIStream to OSIsoft Cloud Services.

::

  POST /api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}  HTTP/1.1
  Authorization: Bearer <bearer-token>
  Content-Length: 139
  Content-Type: application/json
  Host: dat-a.osisoft.com
  {  
     "$id":"1",
     "Id":"Simple",
     "Name":"Simple",
     "Description":null,
     "TypeId":"Simple",
     "BehaviorId":null,
     "Indexes":null 
  }


Step 6: Write data
******************

Qi supports many methods for adding and updating data. In this guide, we will insert. 
Inserts will fail if events with the same index already exist in the database. Update will 
add new events and replace existing events.

To insert an event via the .NET Qi libraries:

::

  Simple value = new Simple()
  {
      Time = DateTime.UtcNow,
      State = State.Ok,
      Measurement = 123.45
  };

  await client.InsertValueAsync(simpleStream.Id, value);

To POST a JSON serialized event to the OSIsoft Cloud Services.

::

  POST /api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/
  InsertValue  HTTP/1.1
  Authorization: Bearer <bearer-token>
  Content-Length: 57
  Content-Type: application/json
  Host: dat-a.osisoft.com
  {  
     "Time":"2017-08-17T17:21:36.3494129Z",
     "State":0,
     "Measurement":123.45
  }

Additional information about writing data can be found in Writing data.


Step 7: Read data
*****************

Qi includes many different read methods for retrieving data from streams. In this guide, 
we will read the value just written.

Reads typically require an index or indexes. Our index is the Time property of Simple. 
Retrieving the distinct value just written will require index, timestamp, of that value.

We Most read calls also require one or more indexes to determine which data to read. 
The simplest way to supply an index is as a string. In .NET a DateTime index for now could be provided as follows:

::

  string index = DateTime.Parse("2017-08-17T17:21:36.3494129Z")
             .ToUniversalTime().ToString("o"); 

To read a value at a distinct index, use the .NET Qi libraries:

::

  value = await client.GetDistinctValueAsync<Simple>(simpleStream.Id, index); 


To read using REST:

::

  GET api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/
        Data/GetDistinctValue?index={index} HTTP/1.1
        
  Authorization: Bearer <bearer-token>
  Content-Length: 0
  Content-Type: 
  Host: dat-a.osisoft.com
      
Additional information about reading data can be found in Reading data.


Handling transient service interruptions
----------------------------------------

All applications that communicate with remote systems must manage transient faults. 
Temporary service interruptions are a fact of life in real-world cloud applications. 

If you access Qi using the Qi .NET libraries, transient fault handling is built in; 
the Qi client automatically retries error codes identified as transient.

If you access the Qi API directly via the OSIsoft Cloud Services endpoint, you should 
consider creating your own retry logic to automatically retry when encountering errors 
identified as transient.

For Qi, the only error you should retry is Http response code 503: service unavailable. 
We recommend an immediate first retry, followed by an exponential back off.


Qi client error
---------------

If you access Qi using the .NET libraries, be aware that any non-success responses returned 
to the client are packaged in a QiHttpClientException, which is an Exception with the following 
additional properties:

::

  string ReasonPhrase
  HttpStatusCode StatusCode
  Dictionary<string, object> Errors 


* The StatusCode provides the HttpStatusCode from the response.
* The ReasonPhrase might provide additional information regarding the cause of the exception. 
  You should always evaluate the ReasonPhrase in addition to the StatusCode to determine the cause of the exception.
* The Errors collection may provide additional specific error information based on the response. For example, 
  if an InsertValues call failed because it conflicted with an existing event in the stream, the index of the 
  conflicting event will be included in this dictionary.

Qi Timeout Request Header
-------------------------

Handling timeout issues can be difficult and confusing in a distributed programming environment. Often, when a client 
times out, the request is terminated before a response is received from the server, resulting in the application being
unaware of the state of the server.

One solution is to use the Request-Timeout header, which is recognized by many OSIsoft Cloud Services. Using the 
header, you can tell the server how long to spend on a particular request before timing out. If possible, the server 
terminates the request if the time it takes to process the request exceeds the timeout value set in the header.

To specify the request timeout value, include the Request-Timeout header and specify the value in seconds.


