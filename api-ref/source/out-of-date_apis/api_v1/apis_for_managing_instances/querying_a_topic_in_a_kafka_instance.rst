:original_name: kafka-api-180614002.html

.. _kafka-api-180614002:

Querying a Topic in a Kafka Instance
====================================

.. note::

   This API is out-of-date and may not be maintained in the future. Please use the API described in :ref:`Listing Topics of a Kafka Instance <listinstancetopics>`.

Function
--------

This API is used to query details about a topic in a Kafka instance.

URI
---

GET /v1.0/{project_id}/instances/{instance_id}/topics

:ref:`Table 1 <kafka-api-180614002__en-us_topic_0128036881_table163952313129>` describes the parameter.

.. _kafka-api-180614002__en-us_topic_0128036881_table163952313129:

.. table:: **Table 1** Parameters

   =========== ====== ========= ==============================
   Parameter   Type   Mandatory Description
   =========== ====== ========= ==============================
   project_id  String Yes       Indicates the ID of a project.
   instance_id String Yes       Indicates the instance ID.
   =========== ====== ========= ==============================

Request
-------

**Request parameters**

None.

**Example request**

.. code-block:: text

   GET https://{dms_endpoint}/v1.0/{project_id}/instances/{instance_id}/topics

Response
--------

**Response parameters**

:ref:`Table 2 <kafka-api-180614002__en-us_topic_0128036881_table2407333125>` describes the response parameter.

.. _kafka-api-180614002__en-us_topic_0128036881_table2407333125:

.. table:: **Table 2** Response parameter

   +-------------------+---------+--------------------------------------------------------------------+
   | Parameter         | Type    | Description                                                        |
   +===================+=========+====================================================================+
   | total             | Integer | Indicates the total number of topics.                              |
   +-------------------+---------+--------------------------------------------------------------------+
   | size              | Integer | Indicates the maximum number of records to be displayed on a page. |
   +-------------------+---------+--------------------------------------------------------------------+
   | remain_partitions | Integer | Indicates the number of remaining partitions.                      |
   +-------------------+---------+--------------------------------------------------------------------+
   | max_partitions    | Integer | Indicates the total number of partitions.                          |
   +-------------------+---------+--------------------------------------------------------------------+
   | topics            | Array   | Indicates the list of topics.                                      |
   +-------------------+---------+--------------------------------------------------------------------+

.. table:: **Table 3** Parameter description

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                               |
   +=======================+=======================+===========================================================================================================================================================================================================+
   | policiesOnly          | Boolean               | Whether this policy is the default policy.                                                                                                                                                                |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | id                    | String                | Indicates the topic name.                                                                                                                                                                                 |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | replication           | Integer               | Indicates the number of replicas, which is configured to ensure data reliability.                                                                                                                         |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | partition             | Integer               | Indicates the number of topic partitions, which is used to set the number of concurrently consumed messages.                                                                                              |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | retention_time        | Integer               | Indicates the retention period of a message.                                                                                                                                                              |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | sync_replication      | Boolean               | Indicates whether to enable synchronous replication. After this function is enabled, the **acks** parameter on the producer client must be set to **-1**. Otherwise, this parameter does not take effect. |
   |                       |                       |                                                                                                                                                                                                           |
   |                       |                       | By default, synchronous replication is disabled.                                                                                                                                                          |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | sync_message_flush    | Boolean               | Indicates whether to enable synchronous flushing. Synchronous flushing compromises performance.                                                                                                           |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | external_configs      | Object                | Indicates the extended configuration.                                                                                                                                                                     |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | topic_type            | Integer               | Indicates the topic type.                                                                                                                                                                                 |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

**Example response**

.. code-block::

   {
    "count": 1,
    "topics": [
     {
      "id": "topic-test",
      "replication": 3,
      "partition": 4,
      "retention_time": 72,
      "sync_replication": "false",
      "sync_message_flush": "false"
     }
    ]
   }

Status Code
-----------

:ref:`Table 4 <kafka-api-180614002__en-us_topic_0128036881_table64308351212>` describes the status code of successful operations. For details about other status codes, see :ref:`Status Code <kafka-api-0034672261>`.

.. _kafka-api-180614002__en-us_topic_0128036881_table64308351212:

.. table:: **Table 4** Status code

   =========== ========================================
   Status Code Description
   =========== ========================================
   200         The information is queried successfully.
   =========== ========================================
