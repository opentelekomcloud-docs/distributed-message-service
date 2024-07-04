:original_name: ShowPartitionEndMessage.html

.. _ShowPartitionEndMessage:

Querying Offset of the Latest Message in a Partition
====================================================

Function
--------

This API is used to query the offset of the latest message in a partition.

URI
---

GET /v2/{project_id}/instances/{instance_id}/management/topics/{topic}/partitions/{partition}/end-message

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

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameters

   +-----------+---------+-----------------------------------------------------------------------------------------+
   | Parameter | Type    | Description                                                                             |
   +===========+=========+=========================================================================================+
   | topic     | String  | Topic name.                                                                             |
   +-----------+---------+-----------------------------------------------------------------------------------------+
   | partition | Integer | Partition number.                                                                       |
   +-----------+---------+-----------------------------------------------------------------------------------------+
   | offset    | Integer | Offset of the latest message.                                                           |
   +-----------+---------+-----------------------------------------------------------------------------------------+
   | timestamp | Long    | Time when a message is created. The value is a Unix timestamp. The unit is millisecond. |
   +-----------+---------+-----------------------------------------------------------------------------------------+

Example Requests
----------------

.. code-block:: text

   GET https://{endpoint}/v2/{project_id}/instances/{instance_id}/management/topics/{topic}/partitions/{partition}/end-message

Example Responses
-----------------

**Status code: 200**

The offset of the latest message in a partition is queried successfully.

.. code-block::

   {
     "topic" : "mytest",
     "partition" : 0,
     "offset" : 9,
     "timestamp" : 1568125039164
   }

Status Codes
------------

+-------------+--------------------------------------------------------------------------+
| Status Code | Description                                                              |
+=============+==========================================================================+
| 200         | The offset of the latest message in a partition is queried successfully. |
+-------------+--------------------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
