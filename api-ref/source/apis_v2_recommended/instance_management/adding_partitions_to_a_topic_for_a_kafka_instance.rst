:original_name: CreatePartition.html

.. _CreatePartition:

Adding Partitions to a Topic for a Kafka Instance
=================================================

Function
--------

This API is used to add partitions to a topic for a Kafka instance.

URI
---

POST /v2/{project_id}/instances/{instance_id}/management/topics/{topic}/partitions-reassignment

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

   +-----------+-----------+---------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Mandatory | Type    | Description                                                                                                                                 |
   +===========+===========+=========+=============================================================================================================================================+
   | partition | No        | Integer | Total number of partitions after the addition. The value must be larger than current number of partitions and smaller than or equal to 100. |
   +-----------+-----------+---------+---------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

None

Example Requests
----------------

.. code-block:: text

   POST https://{endpoint}/v2/{project_id}/instances/{instance_id}/management/topics/{topic}/partitions-reassignment

   {
     "partition" : 3
   }

Example Responses
-----------------

None

Status Codes
------------

=========== ==================================
Status Code Description
=========== ==================================
204         Partitions are added successfully.
=========== ==================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
