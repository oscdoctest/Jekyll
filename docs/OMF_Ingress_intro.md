Data ingress to Cloud Services using OMF

========================================

You can use OSIsoft Message Format (OMF) to achieve high-throughput asynchronous data ingress 
into the OCS data store. The following terms might be useful for understanding the information
in this and subsequent topics:

* A producer of OMF messages intended for OCS is called a *Publisher*. 
* Messages are sent to a queue called a *Topic*. 
* A *Subscription* recieves messages from a Topic and writes them either to the OCS 
  data store or makes them available to an external consumer. 

.. toctree::
   OMF_Ingress_Specification.rst
