:original_name: ListTopicPartitions.html

.. _ListTopicPartitions:

Querying the Partition List of a Topic
======================================

Function
--------

This API is used to query the partition list of a topic.

URI
---

GET /v2/{project_id}/kafka/instances/{instance_id}/topics/{topic}/partitions

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                                               |
   +=============+===========+========+===========================================================================================================+
   | project_id  | Yes       | String | Project ID. For details about how to obtain it, see :ref:`Obtaining a Project ID <kafka-api-0036212547>`. |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                                              |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | topic       | Yes       | String | Topic.                                                                                                    |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+

.. table:: **Table 2** Query Parameters

   +-----------+-----------+---------+--------------------------------------------------------+
   | Parameter | Mandatory | Type    | Description                                            |
   +===========+===========+=========+========================================================+
   | offset    | No        | Integer | Offset. The records after this offset will be queried. |
   +-----------+-----------+---------+--------------------------------------------------------+
   | limit     | No        | Integer | Maximum number of records that can be returned.        |
   +-----------+-----------+---------+--------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +------------+-------------------------------------------------------------------------------+------------------+
   | Parameter  | Type                                                                          | Description      |
   +============+===============================================================================+==================+
   | total      | Integer                                                                       | Total records.   |
   +------------+-------------------------------------------------------------------------------+------------------+
   | partitions | Array of :ref:`partitions <listtopicpartitions__response_partitions>` objects | Partition array. |
   +------------+-------------------------------------------------------------------------------+------------------+

.. _listtopicpartitions__response_partitions:

.. table:: **Table 4** partitions

   ================ ======= ==================================
   Parameter        Type    Description
   ================ ======= ==================================
   partition        Integer Partition ID.
   start_offset     Long    Start offset.
   last_offset      Long    Last offset.
   message_count    Long    Number of messages in a partition.
   last_update_time Long    Last update time.
   ================ ======= ==================================

Example Requests
----------------

Querying the partition list of a topic

.. code-block:: text

   GET https://{endpoint}/v2/{project_id}/kafka/instances/{instance_id}/topics/{topic}/partitions?start=1&limit=10

Example Responses
-----------------

**Status code: 200**

The partition list of the topic is queried successfully.

.. code-block::

   {
     "total" : 3,
     "partitions" : [ {
       "partition" : 0,
       "start_offset" : 0,
       "last_offset" : 1216303,
       "message_count" : 1216303,
       "last_update_time" : 1688011291458
     }, {
       "partition" : 1,
       "start_offset" : 0,
       "last_offset" : 985447,
       "message_count" : 985447,
       "last_update_time" : 1688011291469
     }, {
       "partition" : 2,
       "start_offset" : 0,
       "last_offset" : 923340,
       "message_count" : 923340,
       "last_update_time" : 1688011291526
     } ]
   }

Status Codes
------------

=========== ========================================================
Status Code Description
=========== ========================================================
200         The partition list of the topic is queried successfully.
=========== ========================================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
