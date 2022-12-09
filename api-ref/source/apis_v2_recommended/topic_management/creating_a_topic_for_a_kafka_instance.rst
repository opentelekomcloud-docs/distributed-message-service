:original_name: CreateInstanceTopic.html

.. _CreateInstanceTopic:

Creating a Topic for a Kafka Instance
=====================================

Function
--------

This API is used to create a topic for a Kafka instance.

URI
---

POST /v2/{project_id}/instances/{instance_id}/topics

.. table:: **Table 1** Path Parameters

   =========== ========= ====== ============
   Parameter   Mandatory Type   Description
   =========== ========= ====== ============
   project_id  Yes       String Project ID.
   instance_id Yes       String Instance ID.
   =========== ========= ====== ============

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   +--------------------+-----------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter          | Mandatory | Type    | Description                                                                                                                                                                                      |
   +====================+===========+=========+==================================================================================================================================================================================================+
   | id                 | Yes       | String  | Topic name, which consists of 4 to 64 characters, starts with a letter, and contains only letters, hyphens (-), underscores (_), and digits.                                                     |
   +--------------------+-----------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | replication        | No        | Integer | Number of replicas, which is configured to ensure data reliability. Value range: 1 to 3.                                                                                                         |
   +--------------------+-----------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | sync_message_flush | No        | Boolean | Whether synchronous flushing is enabled. The default value is **false**. Synchronous flushing compromises performance.                                                                           |
   +--------------------+-----------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | partition          | No        | Integer | Number of topic partitions, which is used to set the number of concurrently consumed messages.Value range: 1-100.                                                                                |
   +--------------------+-----------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | sync_replication   | No        | Boolean | Whether synchronous replication is enabled. After this function is enabled, the **acks** parameter on the producer client must be set to **-1**. Otherwise, this parameter does not take effect. |
   +--------------------+-----------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | retention_time     | No        | Integer | Message retention period. The default value is **72**.Value range: 1-720. Unit: hour.                                                                                                            |
   +--------------------+-----------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   name      String Topic name.
   ========= ====== ===========

Example Requests
----------------

.. code-block:: text

   POST https://{endpoint}/v2/{project_id}/instances/{instance_id}/topics

   {
     "id" : "kafka01"
   }

Example Responses
-----------------

**Status code: 200**

The creation is successful.

.. code-block::

   {
     "name" : "kafka01"
   }

Status Codes
------------

=========== ===========================
Status Code Description
=========== ===========================
200         The creation is successful.
=========== ===========================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
