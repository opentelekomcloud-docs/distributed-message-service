:original_name: ShowMessages.html

.. _ShowMessages:

Querying a Message with a Specified Time Period
===============================================

Function
--------

This API is used to query a message with a specified time period.

URI
---

GET /v2/{project_id}/instances/{instance_id}/management/topics/{topic}/messages

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

.. table:: **Table 2** Query Parameters

   +------------+-----------+---------+-----------------------------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type    | Description                                                                                         |
   +============+===========+=========+=====================================================================================================+
   | start_time | No        | String  | Query start time as a Unix timestamp. Default value: **0**.                                         |
   +------------+-----------+---------+-----------------------------------------------------------------------------------------------------+
   | end_time   | No        | String  | Query end time, as a Unix timestamp. Default value: current system time.                            |
   +------------+-----------+---------+-----------------------------------------------------------------------------------------------------+
   | limit      | No        | Integer | Number of messages returned on a page. Default value: **10**.                                       |
   +------------+-----------+---------+-----------------------------------------------------------------------------------------------------+
   | offset     | No        | Integer | Offset, which is the position where the query starts. The value must be greater than or equal to 0. |
   +------------+-----------+---------+-----------------------------------------------------------------------------------------------------+
   | partition  | No        | String  | Partition number. The default value is **-1**, indicating that all partitions are queried.          |
   +------------+-----------+---------+-----------------------------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +----------------+--------------------------------------------------------------------+---------------------------+
   | Parameter      | Type                                                               | Description               |
   +================+====================================================================+===========================+
   | messages       | Array of :ref:`messages <showmessages__response_messages>` objects | Message list.             |
   +----------------+--------------------------------------------------------------------+---------------------------+
   | messages_count | Integer                                                            | Total number of messages. |
   +----------------+--------------------------------------------------------------------+---------------------------+
   | offsets_count  | Integer                                                            | Total number of pages.    |
   +----------------+--------------------------------------------------------------------+---------------------------+
   | offset         | Integer                                                            | Current page.             |
   +----------------+--------------------------------------------------------------------+---------------------------+

.. _showmessages__response_messages:

.. table:: **Table 4** messages

   +-----------------------+-----------------------+---------------------------------------------------------+
   | Parameter             | Type                  | Description                                             |
   +=======================+=======================+=========================================================+
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

   GET https://{endpoint}/v2/{project_id}/instances/{instance_id}/management/topics/{topic}/messages

Example Responses
-----------------

**Status code: 200**

The message with the specified time period is queried successfully.

.. code-block::

   {
     "messages" : [ {
       "topic" : "mytest",
       "partition" : 0,
       "message_offset" : 7,
       "size" : 6,
       "timestamp" : 1568125036045
     } ],
     "messages_count" : 1,
     "offsets_count" : 1,
     "offset" : 1
   }

Status Codes
------------

+-------------+---------------------------------------------------------------------+
| Status Code | Description                                                         |
+=============+=====================================================================+
| 200         | The message with the specified time period is queried successfully. |
+-------------+---------------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
