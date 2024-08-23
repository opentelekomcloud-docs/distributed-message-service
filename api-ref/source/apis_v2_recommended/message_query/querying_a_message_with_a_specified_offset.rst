:original_name: ShowPartitionMessage.html

.. _ShowPartitionMessage:

Querying a Message with a Specified Offset
==========================================

Function
--------

This API is used to query a message with a specified offset.

URI
---

GET /v2/{project_id}/instances/{instance_id}/management/topics/{topic}/partitions/{partition}/message

.. table:: **Table 1** Path Parameters

   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                   |
   +=================+=================+=================+===============================================================================================================+
   | project_id      | Yes             | String          | Project ID. For details about how to obtain it, see :ref:`Obtaining a Project ID <kafka-api-0036212547>`.     |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | instance_id     | Yes             | String          | Instance ID.                                                                                                  |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | topic           | Yes             | String          | Topic name.                                                                                                   |
   |                 |                 |                 |                                                                                                               |
   |                 |                 |                 | A topic name must start with a letter and can only contain letters, hyphens (-), underscores (_), and digits. |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | partition       | Yes             | Integer         | Partition number.                                                                                             |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+

.. table:: **Table 2** Query Parameters

   ============== ========= ====== ===============
   Parameter      Mandatory Type   Description
   ============== ========= ====== ===============
   message_offset Yes       String Message offset.
   ============== ========= ====== ===============

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-----------+----------------------------------------------------------------------------------------------------------------+---------------+
   | Parameter | Type                                                                                                           | Description   |
   +===========+================================================================================================================+===============+
   | message   | Array of :ref:`ShowPartitionMessageEntity <showpartitionmessage__response_showpartitionmessageentity>` objects | Message list. |
   +-----------+----------------------------------------------------------------------------------------------------------------+---------------+

.. _showpartitionmessage__response_showpartitionmessageentity:

.. table:: **Table 4** ShowPartitionMessageEntity

   +-----------------------+-----------------------+---------------------------------------------------------+
   | Parameter             | Type                  | Description                                             |
   +=======================+=======================+=========================================================+
   | key                   | String                | Message key.                                            |
   +-----------------------+-----------------------+---------------------------------------------------------+
   | value                 | String                | Message content.                                        |
   +-----------------------+-----------------------+---------------------------------------------------------+
   | topic                 | String                | Topic name.                                             |
   +-----------------------+-----------------------+---------------------------------------------------------+
   | partition             | Integer               | Partition number.                                       |
   +-----------------------+-----------------------+---------------------------------------------------------+
   | message_offset        | Long                  | Message offset.                                         |
   +-----------------------+-----------------------+---------------------------------------------------------+
   | size                  | Integer               | Message size in bytes.                                  |
   +-----------------------+-----------------------+---------------------------------------------------------+
   | timestamp             | Long                  | Time when a message is created.                         |
   |                       |                       |                                                         |
   |                       |                       | The value is a Unix timestamp. The unit is millisecond. |
   +-----------------------+-----------------------+---------------------------------------------------------+

Example Requests
----------------

.. code-block:: text

   GET https://{endpoint}/v2/{project_id}/instances/{instance_id}/management/topics/{topic}/partitions/{partition}/message?message_offset={message_offset}

Example Responses
-----------------

**Status code: 200**

The message with the specified offset is queried successfully.

.. code-block::

   {
     "message" : [ {
       "topic" : "mytest",
       "partition" : 0,
       "message_offset" : 7,
       "key" : null,
       "value" : "kasjdf",
       "size" : 6,
       "timestamp" : 1568125036045
     } ]
   }

Status Codes
------------

+-------------+----------------------------------------------------------------+
| Status Code | Description                                                    |
+=============+================================================================+
| 200         | The message with the specified offset is queried successfully. |
+-------------+----------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
