:original_name: UpdateInstanceTopic.html

.. _UpdateInstanceTopic:

Modifying Topics of a Kafka Instance
====================================

Function
--------

This API is used to modify topics of a Kafka instance.

URI
---

PUT /v2/{project_id}/instances/{instance_id}/topics

.. table:: **Table 1** Path Parameters

   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                               |
   +=================+=================+=================+===========================================================================================================+
   | project_id      | Yes             | String          | Project ID. For details about how to obtain it, see :ref:`Obtaining a Project ID <kafka-api-0036212547>`. |
   |                 |                 |                 |                                                                                                           |
   |                 |                 |                 | Minimum: **1**                                                                                            |
   |                 |                 |                 |                                                                                                           |
   |                 |                 |                 | Maximum: **64**                                                                                           |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------+
   | instance_id     | Yes             | String          | Instance ID.                                                                                              |
   |                 |                 |                 |                                                                                                           |
   |                 |                 |                 | Minimum: **1**                                                                                            |
   |                 |                 |                 |                                                                                                           |
   |                 |                 |                 | Maximum: **64**                                                                                           |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   +-----------+-----------+----------------------------------------------------------------------+----------------------------+
   | Parameter | Mandatory | Type                                                                 | Description                |
   +===========+===========+======================================================================+============================+
   | topics    | No        | Array of :ref:`topics <updateinstancetopic__request_topics>` objects | Topics that were modified. |
   +-----------+-----------+----------------------------------------------------------------------+----------------------------+

.. _updateinstancetopic__request_topics:

.. table:: **Table 3** topics

   +-----------------------+-----------+------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Parameter             | Mandatory | Type                                                                                           | Description                                 |
   +=======================+===========+================================================================================================+=============================================+
   | id                    | Yes       | String                                                                                         | Topic name, which cannot be modified.       |
   +-----------------------+-----------+------------------------------------------------------------------------------------------------+---------------------------------------------+
   | retention_time        | No        | Integer                                                                                        | Aging time in hour.                         |
   +-----------------------+-----------+------------------------------------------------------------------------------------------------+---------------------------------------------+
   | sync_replication      | No        | Boolean                                                                                        | Whether synchronous replication is enabled. |
   +-----------------------+-----------+------------------------------------------------------------------------------------------------+---------------------------------------------+
   | sync_message_flush    | No        | Boolean                                                                                        | Whether synchronous flushing is enabled.    |
   +-----------------------+-----------+------------------------------------------------------------------------------------------------+---------------------------------------------+
   | new_partition_numbers | No        | Integer                                                                                        | Number of the partitions.                   |
   +-----------------------+-----------+------------------------------------------------------------------------------------------------+---------------------------------------------+
   | new_partition_brokers | No        | Array of integers                                                                              | Specifying brokers for new partitions.      |
   +-----------------------+-----------+------------------------------------------------------------------------------------------------+---------------------------------------------+
   | topic_other_configs   | No        | Array of :ref:`topic_other_configs <updateinstancetopic__request_topic_other_configs>` objects | Topic configuration.                        |
   +-----------------------+-----------+------------------------------------------------------------------------------------------------+---------------------------------------------+
   | topic_desc            | No        | String                                                                                         | Topic description.                          |
   +-----------------------+-----------+------------------------------------------------------------------------------------------------+---------------------------------------------+

.. _updateinstancetopic__request_topic_other_configs:

.. table:: **Table 4** topic_other_configs

   ========= ========= ====== ====================
   Parameter Mandatory Type   Description
   ========= ========= ====== ====================
   name      No        String Configuration name.
   value     No        String Configuration value.
   ========= ========= ====== ====================

Response Parameters
-------------------

None

Example Requests
----------------

Modifying parameters of topic-1284340884. Specifically, change the aging time to 72 hours, the number of partitions to 6, timestamp to LogAppendTime, max. batch size to 10485760, specify new partitions on broker-1 and broker-2, and disable synchronous replication and flushing.

.. code-block:: text

   PUT https://{endpoint}/v2/{project_id}/instances/{instance_id}/topics

   {
     "topics" : [ {
       "id" : "test01",
       "retention_time" : 72,
       "sync_replication" : false,
       "sync_message_flush" : false,
       "new_partition_numbers" : 6,
       "new_partition_brokers" : [ 1, 2 ],
       "topic_other_configs" : [ {
         "name" : "message.timestamp.type",
         "value" : "LogAppendTime"
       }, {
         "name" : "max.message.bytes",
         "value" : 10485760
       } ],
       "topic_desc" : "This is a test topic"
     } ]
   }

Example Responses
-----------------

None

Status Codes
------------

=========== ===============================
Status Code Description
=========== ===============================
204         The modification is successful.
=========== ===============================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
