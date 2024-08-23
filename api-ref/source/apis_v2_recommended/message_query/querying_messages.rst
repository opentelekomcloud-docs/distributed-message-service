:original_name: ShowInstanceMessages.html

.. _ShowInstanceMessages:

Querying Messages
=================

Function
--------

This API is used to query the offset and content of a message.

This API queries the message offset based on the timestamp and then queries the message content based on the offset.

URI
---

GET /v2/{project_id}/instances/{instance_id}/messages

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                                               |
   +=============+===========+========+===========================================================================================================+
   | project_id  | Yes       | String | Project ID. For details about how to obtain it, see :ref:`Obtaining a Project ID <kafka-api-0036212547>`. |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                                              |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+

.. table:: **Table 2** Query Parameters

   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                   |
   +=================+=================+=================+===============================================================================================================+
   | topic           | Yes             | String          | Topic name.                                                                                                   |
   |                 |                 |                 |                                                                                                               |
   |                 |                 |                 | A topic name must start with a letter and can only contain letters, hyphens (-), underscores (_), and digits. |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | asc             | No              | Boolean         | Whether to sort messages by time.                                                                             |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | start_time      | No              | String          | Start time.                                                                                                   |
   |                 |                 |                 |                                                                                                               |
   |                 |                 |                 | The value is a Unix timestamp, in millisecond.                                                                |
   |                 |                 |                 |                                                                                                               |
   |                 |                 |                 | This parameter is mandatory when you query the message offset.                                                |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | end_time        | No              | String          | End time.                                                                                                     |
   |                 |                 |                 |                                                                                                               |
   |                 |                 |                 | The value is a Unix timestamp, in millisecond.                                                                |
   |                 |                 |                 |                                                                                                               |
   |                 |                 |                 | This parameter is mandatory when you query the message offset.                                                |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | limit           | No              | String          | Number of messages displayed on each page.                                                                    |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | offset          | No              | String          | Page number.                                                                                                  |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | download        | No              | Boolean         | Whether download is required.                                                                                 |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | message_offset  | No              | String          | Message offset.                                                                                               |
   |                 |                 |                 |                                                                                                               |
   |                 |                 |                 | **This parameter is mandatory when you query the message content.**                                           |
   |                 |                 |                 |                                                                                                               |
   |                 |                 |                 | If **start_time** and **end_time** are not empty, this parameter is invalid.                                  |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | partition       | No              | String          | Partition.                                                                                                    |
   |                 |                 |                 |                                                                                                               |
   |                 |                 |                 | **This parameter is mandatory when you query the message content.**                                           |
   |                 |                 |                 |                                                                                                               |
   |                 |                 |                 | If **start_time** and **end_time** are not empty, this parameter is invalid.                                  |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | keyword         | No              | String          | Keyword.                                                                                                      |
   |                 |                 |                 |                                                                                                               |
   |                 |                 |                 | The value ranges from 0 to 50.                                                                                |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-----------+----------------------------------------------------------------------------------------+---------------------------------+
   | Parameter | Type                                                                                   | Description                     |
   +===========+========================================================================================+=================================+
   | messages  | Array of :ref:`MessagesEntity <showinstancemessages__response_messagesentity>` objects | Message list.                   |
   +-----------+----------------------------------------------------------------------------------------+---------------------------------+
   | total     | Long                                                                                   | Total number of messages.       |
   +-----------+----------------------------------------------------------------------------------------+---------------------------------+
   | size      | Long                                                                                   | Number of records on each page. |
   +-----------+----------------------------------------------------------------------------------------+---------------------------------+

.. _showinstancemessages__response_messagesentity:

.. table:: **Table 4** MessagesEntity

   +----------------+---------+----------------------------------------------------------------+
   | Parameter      | Type    | Description                                                    |
   +================+=========+================================================================+
   | topic          | String  | Topic name.                                                    |
   +----------------+---------+----------------------------------------------------------------+
   | partition      | Integer | Partition where the message is located.                        |
   +----------------+---------+----------------------------------------------------------------+
   | key            | String  | Message key.                                                   |
   +----------------+---------+----------------------------------------------------------------+
   | value          | String  | Message content.                                               |
   +----------------+---------+----------------------------------------------------------------+
   | size           | Integer | Message size.                                                  |
   +----------------+---------+----------------------------------------------------------------+
   | timestamp      | Long    | Message production time. The value is a UNIX timestamp, in ms. |
   +----------------+---------+----------------------------------------------------------------+
   | huge_message   | Boolean | Big data flag.                                                 |
   +----------------+---------+----------------------------------------------------------------+
   | message_offset | Long    | Message offset.                                                |
   +----------------+---------+----------------------------------------------------------------+
   | message_id     | String  | Message ID.                                                    |
   +----------------+---------+----------------------------------------------------------------+
   | app_id         | String  | Application ID.                                                |
   +----------------+---------+----------------------------------------------------------------+
   | tag            | String  | Message label.                                                 |
   +----------------+---------+----------------------------------------------------------------+

**Status code: 400**

.. table:: **Table 5** Response body parameters

   ========== ====== ==================
   Parameter  Type   Description
   ========== ====== ==================
   error_code String Error code.
   error_msg  String Error description.
   ========== ====== ==================

**Status code: 403**

.. table:: **Table 6** Response body parameters

   ========== ====== ==================
   Parameter  Type   Description
   ========== ====== ==================
   error_code String Error code.
   error_msg  String Error description.
   ========== ====== ==================

Example Requests
----------------

-  Querying the message offset.

   .. code-block:: text

      GET https://{endpoint}/v2/{project_id}/instances/{instance_id}/messages?asc=false&end_time=1608609032042&limit=10&offset=0&start_time=1608608432042&topic=topic-test

-  Querying the message content.

   .. code-block:: text

      GET https://{endpoint}/v2/{project_id}/instances/{instance_id}/messages?download=false&message_offset=0&partition=0&topic=topic-test

Example Responses
-----------------

**Status code: 200**

The query is successful.

.. code-block::

   {
     "messages" : [ {
       "topic" : "topic-test",
       "partition" : 0,
       "value" : "hello world",
       "size" : 21,
       "timestamp" : 1607598463502,
       "huge_message" : false,
       "message_offset" : 4,
       "message_id" : "",
       "app_id" : "",
       "tag" : ""
     } ],
     "total" : 1,
     "size" : 1
   }

Status Codes
------------

=========== ========================
Status Code Description
=========== ========================
200         The query is successful.
400         Invalid parameters.
403         Authentication failed.
=========== ========================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
