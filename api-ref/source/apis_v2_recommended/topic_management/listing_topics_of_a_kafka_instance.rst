:original_name: ListInstanceTopics.html

.. _ListInstanceTopics:

Listing Topics of a Kafka Instance
==================================

Function
--------

This API is used to query details about topics of a Kafka instance.

URI
---

GET /v2/{project_id}/instances/{instance_id}/topics

.. table:: **Table 1** Path Parameters

   =========== ========= ====== ============
   Parameter   Mandatory Type   Description
   =========== ========= ====== ============
   project_id  Yes       String Project ID.
   instance_id Yes       String Instance ID.
   =========== ========= ====== ============

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameters

   +-------------------+--------------------------------------------------------------------------------+------------------------------------------------------+
   | Parameter         | Type                                                                           | Description                                          |
   +===================+================================================================================+======================================================+
   | total             | Integer                                                                        | Total number of topics.                              |
   +-------------------+--------------------------------------------------------------------------------+------------------------------------------------------+
   | size              | Integer                                                                        | Maximum number of records to be displayed on a page. |
   +-------------------+--------------------------------------------------------------------------------+------------------------------------------------------+
   | remain_partitions | Integer                                                                        | Number of remaining partitions.                      |
   +-------------------+--------------------------------------------------------------------------------+------------------------------------------------------+
   | max_partitions    | Integer                                                                        | Total number of partitions.                          |
   +-------------------+--------------------------------------------------------------------------------+------------------------------------------------------+
   | topics            | Array of :ref:`TopicEntity <listinstancetopics__response_topicentity>` objects | Topic list.                                          |
   +-------------------+--------------------------------------------------------------------------------+------------------------------------------------------+

.. _listinstancetopics__response_topicentity:

.. table:: **Table 3** TopicEntity

   +--------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter          | Type    | Description                                                                                                                                                                                      |
   +====================+=========+==================================================================================================================================================================================================+
   | policiesOnly       | Boolean | Whether this policy is the default policy.                                                                                                                                                       |
   +--------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | name               | String  | Topic name.                                                                                                                                                                                      |
   +--------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | replication        | Integer | Number of replicas, which is configured to ensure data reliability.                                                                                                                              |
   +--------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | partition          | Integer | Number of topic partitions, which is used to set the number of concurrently consumed messages.                                                                                                   |
   +--------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | retention_time     | Integer | Retention period of a message.                                                                                                                                                                   |
   +--------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | sync_replication   | Boolean | Whether synchronous replication is enabled. After this function is enabled, the **acks** parameter on the producer client must be set to **-1**. Otherwise, this parameter does not take effect. |
   +--------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | sync_message_flush | Boolean | Whether synchronous flushing is enabled. The default value is **false**. Synchronous flushing compromises performance.                                                                           |
   +--------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | external_configs   | Object  | Extended configuration.                                                                                                                                                                          |
   +--------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | topic_type         | Integer | Topic type. Options: **0**: common topic; **1**: system (internal) topic.                                                                                                                        |
   +--------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Example Requests
----------------

.. code-block:: text

   GET https://{endpoint}/v2/{project_id}/instances/{instance_id}/topics

Example Responses
-----------------

**Status code: 200**

The query is successful.

.. code-block::

   {
     "total" : 3,
     "size" : 3,
     "topics" : [ {
       "policiesOnly" : false,
       "name" : "topic-11",
       "replication" : 3,
       "partition" : 3,
       "retention_time" : 72,
       "sync_replication" : false,
       "sync_message_flush" : false,
       "external_configs" : { },
       "topic_type" : 0
     }, {
       "policiesOnly" : false,
       "name" : "topic-2077405901",
       "replication" : 3,
       "partition" : 3,
       "retention_time" : 72,
       "sync_replication" : false,
       "sync_message_flush" : true,
       "external_configs" : { },
       "topic_type" : 0
     }, {
       "policiesOnly" : false,
       "name" : "topic-test",
       "replication" : 3,
       "partition" : 3,
       "retention_time" : 1,
       "sync_replication" : true,
       "sync_message_flush" : false,
       "external_configs" : { },
       "topic_type" : 0
     } ]
   }

Status Codes
------------

=========== ========================
Status Code Description
=========== ========================
200         The query is successful.
=========== ========================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
