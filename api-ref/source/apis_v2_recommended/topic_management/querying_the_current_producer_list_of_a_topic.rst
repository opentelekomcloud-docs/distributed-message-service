:original_name: ListTopicProducers.html

.. _ListTopicProducers:

Querying the Current Producer List of a Topic
=============================================

Function
--------

This API is used to query the current producer list of a topic.

URI
---

GET /v2/{project_id}/kafka/instances/{instance_id}/topics/{topic}/producers

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
   | topic           | Yes             | String          | Topic.                                                                                                    |
   |                 |                 |                 |                                                                                                           |
   |                 |                 |                 | Minimum: **1**                                                                                            |
   |                 |                 |                 |                                                                                                           |
   |                 |                 |                 | Maximum: **200**                                                                                          |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------+

.. table:: **Table 2** Query Parameters

   +-----------------+-----------------+-----------------+--------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                            |
   +=================+=================+=================+========================================================+
   | offset          | No              | Integer         | Offset. The records after this offset will be queried. |
   |                 |                 |                 |                                                        |
   |                 |                 |                 | Minimum: **0**                                         |
   |                 |                 |                 |                                                        |
   |                 |                 |                 | Maximum: **10000**                                     |
   +-----------------+-----------------+-----------------+--------------------------------------------------------+
   | limit           | No              | Integer         | Maximum number of records that can be returned.        |
   |                 |                 |                 |                                                        |
   |                 |                 |                 | Minimum: **1**                                         |
   |                 |                 |                 |                                                        |
   |                 |                 |                 | Maximum: **50**                                        |
   +-----------------+-----------------+-----------------+--------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-----------------------+----------------------------------------------------------------------------+--------------------------+
   | Parameter             | Type                                                                       | Description              |
   +=======================+============================================================================+==========================+
   | total                 | Integer                                                                    | Total records.           |
   |                       |                                                                            |                          |
   |                       |                                                                            | Minimum: **0**           |
   |                       |                                                                            |                          |
   |                       |                                                                            | Maximum: **10000**       |
   +-----------------------+----------------------------------------------------------------------------+--------------------------+
   | producers             | Array of :ref:`producers <listtopicproducers__response_producers>` objects | Producer list.           |
   |                       |                                                                            |                          |
   |                       |                                                                            | Array Length: **0 - 50** |
   +-----------------------+----------------------------------------------------------------------------+--------------------------+

.. _listtopicproducers__response_producers:

.. table:: **Table 4** producers

   +-----------------------+-----------------------+-------------------------------------+
   | Parameter             | Type                  | Description                         |
   +=======================+=======================+=====================================+
   | producer_address      | String                | Producer address.                   |
   |                       |                       |                                     |
   |                       |                       | Minimum: **0**                      |
   |                       |                       |                                     |
   |                       |                       | Maximum: **64**                     |
   +-----------------------+-----------------------+-------------------------------------+
   | broker_address        | String                | Broker address.                     |
   |                       |                       |                                     |
   |                       |                       | Minimum: **0**                      |
   |                       |                       |                                     |
   |                       |                       | Maximum: **64**                     |
   +-----------------------+-----------------------+-------------------------------------+
   | join_time             | Long                  | Time when the broker was connected. |
   |                       |                       |                                     |
   |                       |                       | Minimum: **0**                      |
   |                       |                       |                                     |
   |                       |                       | Maximum: **9223372036854775807**    |
   +-----------------------+-----------------------+-------------------------------------+

Example Requests
----------------

Querying the current producer list of a topic

.. code-block:: text

   GET https://{endpoint}/v2/{project_id}/kafka/instances/{instance_id}/topics/{topic}/producers?offset=0&limit=10

Example Responses
-----------------

**Status code: 200**

The current producer list of the topic is queried successfully.

.. code-block::

   {
     "total" : 3,
     "producers" : [ {
       "producer_address" : "192.0.0.149:40443",
       "broker_address" : "192.0.0.146:9092",
       "join_time" : 1687204743328
     }, {
       "producer_address" : "192.0.0.149:13807",
       "broker_address" : "192.0.0.80:9092",
       "join_time" : 1687204745939
     }, {
       "producer_address" : "192.0.0.149:31876",
       "broker_address" : "192.0.0.71:9092",
       "join_time" : 1687204744934
     } ]
   }

Status Codes
------------

+-------------+-----------------------------------------------------------------+
| Status Code | Description                                                     |
+=============+=================================================================+
| 200         | The current producer list of the topic is queried successfully. |
+-------------+-----------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
