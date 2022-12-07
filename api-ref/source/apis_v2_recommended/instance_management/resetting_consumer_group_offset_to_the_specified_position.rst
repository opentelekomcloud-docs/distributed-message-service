:original_name: ResetMessageOffset.html

.. _ResetMessageOffset:

Resetting Consumer Group Offset to the Specified Position
=========================================================

Function
--------

Kafka instances do not support resetting the consumer offset online. Before resetting, stop the client for which the offset is to be reset.> After a client is stopped, the server considers the client offline only after the time period specified in **ConsumerConfig.SESSION_TIMEOUT_MS_CONFIG** (1000 ms by default).

URI
---

POST /v2/{project_id}/instances/{instance_id}/management/groups/{group}/reset-message-offset

.. table:: **Table 1** Path Parameters

   =========== ========= ====== ====================
   Parameter   Mandatory Type   Description
   =========== ========= ====== ====================
   project_id  Yes       String Project ID.
   instance_id Yes       String Instance ID.
   group       Yes       String Consumer group name.
   =========== ========= ====== ====================

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                         |
   +=================+=================+=================+=====================================================================================================================+
   | topic           | Yes             | String          | Topic name.                                                                                                         |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
   | partition       | No              | Integer         | Partition number. The default value is **-1**, indicating that all partitions are reset.                            |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
   | message_offset  | No              | Integer         | Resetting consumer group offset to the specified position.                                                          |
   |                 |                 |                 |                                                                                                                     |
   |                 |                 |                 | -  If this position is earlier than the current earliest offset, the offset will be reset to the earliest offset.   |
   |                 |                 |                 |                                                                                                                     |
   |                 |                 |                 | -  If this offset is later than the current largest offset, the offset will be reset to the latest offset.          |
   |                 |                 |                 |                                                                                                                     |
   |                 |                 |                 | **Either message_offset or timestamp must be specified.**                                                           |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
   | timestamp       | No              | Integer         | Specified time that the offset is to be reset to. The value is a Unix timestamp, in millisecond.                    |
   |                 |                 |                 |                                                                                                                     |
   |                 |                 |                 | -  If this time is earlier than the current earliest timestamp, the offset will be reset to the earliest timestamp. |
   |                 |                 |                 |                                                                                                                     |
   |                 |                 |                 | -  If this time is later than the current largest timestamp, the offset will be reset to the latest timestamp.      |
   |                 |                 |                 |                                                                                                                     |
   |                 |                 |                 | **Either message_offset or timestamp must be specified.**                                                           |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

None

Example Requests
----------------

-  Resetting consumer group offset to the specified position.

   .. code-block:: text

      POST https://{endpoint}/v2/{project_id}/instances/{instance_id}/management/groups/{group}/reset-message-offset

      {
        "topic" : "test",
        "partition" : 0,
        "message_offset" : 10
      }

-  Resetting consumer group offset to the specified time.

   .. code-block:: text

      POST https://{endpoint}/v2/{project_id}/instances/{instance_id}/management/groups/{group}/reset-message-offset

      {
        "topic" : "test",
        "partition" : 0,
        "timestamp" : 1571812144000
      }

Example Responses
-----------------

None

Status Codes
------------

+-------------+----------------------------------------------------------------------------+
| Status Code | Description                                                                |
+=============+============================================================================+
| 204         | The consumer group offset is successfully reset to the specified position. |
+-------------+----------------------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
