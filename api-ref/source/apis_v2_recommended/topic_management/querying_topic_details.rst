:original_name: ShowInstanceTopicDetail.html

.. _ShowInstanceTopicDetail:

Querying Topic Details
======================

Function
--------

This API is used to query topic details of a Kafka instance. (Up to 1s for each instance call)

URI
---

GET /v2/{project_id}/instances/{instance_id}/management/topics/{topic}

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                                               |
   +=============+===========+========+===========================================================================================================+
   | project_id  | Yes       | String | Project ID. For details about how to obtain it, see :ref:`Obtaining a Project ID <kafka-api-0036212547>`. |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                                              |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | topic       | Yes       | String | Topic name.                                                                                               |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameters

   +------------------+-----------------------------------------------------------------------------------+------------------------------------------------------+
   | Parameter        | Type                                                                              | Description                                          |
   +==================+===================================================================================+======================================================+
   | topic            | String                                                                            | Topic name.                                          |
   +------------------+-----------------------------------------------------------------------------------+------------------------------------------------------+
   | partitions       | Array of :ref:`partitions <showinstancetopicdetail__response_partitions>` objects | Partition list.                                      |
   +------------------+-----------------------------------------------------------------------------------+------------------------------------------------------+
   | group_subscribed | Array of strings                                                                  | List of consumer groups that subscribe to the topic. |
   +------------------+-----------------------------------------------------------------------------------+------------------------------------------------------+

.. _showinstancetopicdetail__response_partitions:

.. table:: **Table 3** partitions

   +-----------------------+-------------------------------------------------------------------------------+----------------------------------------------------------+
   | Parameter             | Type                                                                          | Description                                              |
   +=======================+===============================================================================+==========================================================+
   | partition             | Integer                                                                       | Partition ID.                                            |
   +-----------------------+-------------------------------------------------------------------------------+----------------------------------------------------------+
   | leader                | Integer                                                                       | ID of the broker where the leader replica resides.       |
   +-----------------------+-------------------------------------------------------------------------------+----------------------------------------------------------+
   | leo                   | Integer                                                                       | LEO of the partition leader replica.                     |
   +-----------------------+-------------------------------------------------------------------------------+----------------------------------------------------------+
   | hw                    | Integer                                                                       | High watermark (HW) of the partition.                    |
   +-----------------------+-------------------------------------------------------------------------------+----------------------------------------------------------+
   | lso                   | Integer                                                                       | Log start offset (LSO) of the partition leader replica.  |
   +-----------------------+-------------------------------------------------------------------------------+----------------------------------------------------------+
   | last_update_timestamp | Long                                                                          | Time when the last message was written to the partition. |
   |                       |                                                                               |                                                          |
   |                       |                                                                               | The value is a Unix timestamp.                           |
   |                       |                                                                               |                                                          |
   |                       |                                                                               | Unit: ms                                                 |
   +-----------------------+-------------------------------------------------------------------------------+----------------------------------------------------------+
   | replicas              | Array of :ref:`replicas <showinstancetopicdetail__response_replicas>` objects | Replica list.                                            |
   +-----------------------+-------------------------------------------------------------------------------+----------------------------------------------------------+

.. _showinstancetopicdetail__response_replicas:

.. table:: **Table 4** replicas

   +-----------+---------+-----------------------------------------------------------------------+
   | Parameter | Type    | Description                                                           |
   +===========+=========+=======================================================================+
   | broker    | Integer | ID of the broker where the replica resides.                           |
   +-----------+---------+-----------------------------------------------------------------------+
   | leader    | Boolean | Whether the replica is the leader.                                    |
   +-----------+---------+-----------------------------------------------------------------------+
   | in_sync   | Boolean | Whether the replica is in the ISR.                                    |
   +-----------+---------+-----------------------------------------------------------------------+
   | size      | Integer | Current log size of the replica. Unit: byte.                          |
   +-----------+---------+-----------------------------------------------------------------------+
   | lag       | Long    | Number of messages that lag behind the high watermark in the replica. |
   +-----------+---------+-----------------------------------------------------------------------+

Example Requests
----------------

Querying details about a specified topic

.. code-block:: text

   GET https://{endpoint}/v2/{project_id}/instances/{instance_id}/management/topics/{topic}

Example Responses
-----------------

**Status code: 200**

The query is successful.

.. code-block::

   {
     "topic" : "test",
     "partitions" : [ {
       "partition" : 0,
       "leader" : 2,
       "replicas" : [ {
         "broker" : 2,
         "leader" : true,
         "in_sync" : true,
         "size" : 123971146,
         "lag" : 0
       }, {
         "broker" : 1,
         "leader" : false,
         "in_sync" : true,
         "size" : 123971146,
         "lag" : 0
       }, {
         "broker" : 0,
         "leader" : false,
         "in_sync" : true,
         "size" : 123971146,
         "lag" : 0
       } ],
       "lso" : 0,
       "leo" : 13598,
       "hw" : 13598,
       "last_update_timestamp" : 1571477180985
     }, {
       "partition" : 2,
       "leader" : 1,
       "replicas" : [ {
         "broker" : 1,
         "leader" : true,
         "in_sync" : true,
         "size" : 123889531,
         "lag" : 0
       }, {
         "broker" : 0,
         "leader" : false,
         "in_sync" : true,
         "size" : 123889531,
         "lag" : 0
       }, {
         "broker" : 2,
         "leader" : false,
         "in_sync" : true,
         "size" : 123889531,
         "lag" : 0
       } ],
       "lso" : 0,
       "leo" : 13601,
       "hw" : 13601,
       "last_update_timestamp" : 1571477077146
     }, {
       "partition" : 1,
       "leader" : 0,
       "replicas" : [ {
         "broker" : 0,
         "leader" : true,
         "in_sync" : true,
         "size" : 127245604,
         "lag" : 0
       }, {
         "broker" : 2,
         "leader" : false,
         "in_sync" : true,
         "size" : 127245604,
         "lag" : 0
       }, {
         "broker" : 1,
         "leader" : false,
         "in_sync" : true,
         "size" : 127245604,
         "lag" : 0
       } ],
       "lso" : 0,
       "leo" : 13599,
       "hw" : 13599,
       "last_update_timestamp" : 1571477172959
     } ],
     "group_subscribed" : [ "test-consumer-group" ]
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
