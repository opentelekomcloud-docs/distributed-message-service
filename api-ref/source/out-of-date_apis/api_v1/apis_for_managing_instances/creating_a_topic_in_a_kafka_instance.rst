:original_name: kafka-api-180614001.html

.. _kafka-api-180614001:

Creating a Topic in a Kafka Instance
====================================

.. note::

   This API is out-of-date and may not be maintained in the future. Please use the API described in :ref:`Creating a Topic for a Kafka Instance <createinstancetopic>`.

Function
--------

This API is used to create a topic in a Kafka instance.

URI
---

POST /v1.0/{project_id}/instances/{instance_id}/topics

:ref:`Table 1 <kafka-api-180614001__en-us_topic_0128036928_table5338194611119>` describes the parameters.

.. _kafka-api-180614001__en-us_topic_0128036928_table5338194611119:

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

:ref:`Table 2 <kafka-api-180614001__en-us_topic_0128036928_table14347154691119>` describes the parameter.

.. _kafka-api-180614001__en-us_topic_0128036928_table14347154691119:

.. table:: **Table 2** Request parameters

   +--------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter          | Type            | Mandatory       | Description                                                                                                                                                                                               |
   +====================+=================+=================+===========================================================================================================================================================================================================+
   | id                 | String          | Yes             | Indicates the name of a topic. A topic name consists of 4 to 64 characters, starts with a letter, and contains only letters, hyphens (-), underscores (_), and digits.                                    |
   +--------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | partition          | Integer         | No              | Indicates the number of topic partitions, which is used to set the number of concurrently consumed messages.                                                                                              |
   |                    |                 |                 |                                                                                                                                                                                                           |
   |                    |                 |                 | Value range: 1-100. Default value: **3**.                                                                                                                                                                 |
   +--------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | replication        | Integer         | No              | Indicates the number of replicas, which is configured to ensure data reliability.                                                                                                                         |
   |                    |                 |                 |                                                                                                                                                                                                           |
   |                    |                 |                 | Value range: 1-3. Default value: **3**.                                                                                                                                                                   |
   +--------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | sync_replication   | Boolean         | No              | Indicates whether to enable synchronous replication. After this function is enabled, the **acks** parameter on the producer client must be set to **-1**. Otherwise, this parameter does not take effect. |
   |                    |                 |                 |                                                                                                                                                                                                           |
   |                    |                 |                 | By default, synchronous replication is disabled.                                                                                                                                                          |
   +--------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | retention_time     | Integer         | No              | Indicates the retention period of a message. Its default value is **72**.                                                                                                                                 |
   |                    |                 |                 |                                                                                                                                                                                                           |
   |                    |                 |                 | Value range: 1-720. Unit: hour.                                                                                                                                                                           |
   +--------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | sync_message_flush | Boolean         | No              | Indicates whether to enable synchronous flushing. Default value: **false**. Synchronous flushing compromises performance.                                                                                 |
   +--------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

**Example request**

.. code-block:: text

   POST https://{dms_endpoint}/v1.0/{project_id}/instances/{instance_id}/topics
   {
     "id" : "haha",
     "partition" : 3,
     "replication" : 3,
     "sync_replication " : true,
     "retention_time" : 10,
     "sync_message_flush" : true
   }

Response
--------

**Response parameters**

:ref:`Table 3 <kafka-api-180614001__en-us_topic_0128036928_table113758463117>` describes the parameter.

.. _kafka-api-180614001__en-us_topic_0128036928_table113758463117:

.. table:: **Table 3** Response parameters

   ========= ====== ==============================
   Parameter Type   Description
   ========= ====== ==============================
   id        String Indicates the name of a topic.
   ========= ====== ==============================

**Example response**

.. code-block::

   {
   "id": "haha"
   }

Status Code
-----------

:ref:`Table 4 <kafka-api-180614001__en-us_topic_0128036928_table4381154610118>` describes the status code of successful operations. For details about other status codes, see :ref:`Status Code <kafka-api-0034672261>`.

.. _kafka-api-180614001__en-us_topic_0128036928_table4381154610118:

.. table:: **Table 4** Status code

   =========== ==================================
   Status Code Description
   =========== ==================================
   200         The topic is created successfully.
   =========== ==================================
