:original_name: UpdateTopicReplica.html

.. _UpdateTopicReplica:

Reassigning Replicas of a Topic for a Kafka Instance
====================================================

Function
--------

This API is used to reassign replicas of a topic for a Kafka instance.

URI
---

POST /v2/{project_id}/instances/{instance_id}/management/topics/{topic}/replicas-reassignment

.. table:: **Table 1** Path Parameters

   =========== ========= ====== ============
   Parameter   Mandatory Type   Description
   =========== ========= ====== ============
   project_id  Yes       String Project ID.
   instance_id Yes       String Instance ID.
   topic       Yes       String Topic name.
   =========== ========= ====== ============

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   +------------+-----------+-----------------------------------------------------------------------------+-----------------------------------------------------------+
   | Parameter  | Mandatory | Type                                                                        | Description                                               |
   +============+===========+=============================================================================+===========================================================+
   | partitions | No        | Array of :ref:`partitions <updatetopicreplica__request_partitions>` objects | Assignment of replicas of the partition after the change. |
   +------------+-----------+-----------------------------------------------------------------------------+-----------------------------------------------------------+

.. _updatetopicreplica__request_partitions:

.. table:: **Table 3** partitions

   +-----------+-----------+-------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Mandatory | Type              | Description                                                                                                                                                                                                                                                 |
   +===========+===========+===================+=============================================================================================================================================================================================================================================================+
   | partition | No        | Integer           | Partition ID.                                                                                                                                                                                                                                               |
   +-----------+-----------+-------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | replicas  | No        | Array of integers | ID of the broker where the replica is expected to reside. The first integer in the array represents the leader replica broker ID. All partitions must have the same number of replicas. The number of replicas cannot be larger than the number of brokers. |
   +-----------+-----------+-------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

None

Example Requests
----------------

.. code-block:: text

   POST https://{endpoint}/v2/{project_id}/instances/{instance_id}/management/topics/{topic}/replicas-reassignment

   {
     "partitions" : [ {
       "partition" : 1,
       "replicas" : [ 1, 2 ]
     }, {
       "partition" : 0,
       "replicas" : [ 0, 1 ]
     } ]
   }

Example Responses
-----------------

None

Status Codes
------------

=========== =========================================
Status Code Description
=========== =========================================
204         The replicas are reassigned successfully.
=========== =========================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
