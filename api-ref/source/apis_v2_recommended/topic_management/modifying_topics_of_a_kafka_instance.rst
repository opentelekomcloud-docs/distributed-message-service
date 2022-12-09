:original_name: UpdateInstanceTopic.html

.. _UpdateInstanceTopic:

Modifying Topics of a Kafka Instance
====================================

Function
--------

This API is used to modify topics of a Kafka instance.

URI
---

PUT /v2/{project_id}/instances/{instance_id}/topics

.. table:: **Table 1** Path Parameters

   =========== ========= ====== ============
   Parameter   Mandatory Type   Description
   =========== ========= ====== ============
   project_id  Yes       String Project ID.
   instance_id Yes       String Instance ID.
   =========== ========= ====== ============

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   +-----------+-----------+----------------------------------------------------------------------+----------------------------+
   | Parameter | Mandatory | Type                                                                 | Description                |
   +===========+===========+======================================================================+============================+
   | topics    | No        | Array of :ref:`topics <updateinstancetopic__request_topics>` objects | Topics that were modified. |
   +-----------+-----------+----------------------------------------------------------------------+----------------------------+

.. _updateinstancetopic__request_topics:

.. table:: **Table 3** topics

   +-----------------------+-----------+---------+---------------------------------------------+
   | Parameter             | Mandatory | Type    | Description                                 |
   +=======================+===========+=========+=============================================+
   | id                    | Yes       | String  | Topic name, which cannot be modified.       |
   +-----------------------+-----------+---------+---------------------------------------------+
   | retention_time        | No        | Integer | Aging time in hour.                         |
   +-----------------------+-----------+---------+---------------------------------------------+
   | sync_replication      | No        | Boolean | Whether synchronous replication is enabled. |
   +-----------------------+-----------+---------+---------------------------------------------+
   | sync_message_flush    | No        | Boolean | Whether synchronous flushing is enabled.    |
   +-----------------------+-----------+---------+---------------------------------------------+
   | new_partition_numbers | No        | Integer | Number of the partitions.                   |
   +-----------------------+-----------+---------+---------------------------------------------+

Response Parameters
-------------------

None

Example Requests
----------------

.. code-block:: text

   PUT https://{endpoint}/v2/{project_id}/instances/{instance_id}/topics

   {
     "topics" : [ {
       "id" : "topic-1284340884",
       "retention_time" : 70,
       "sync_replication" : false,
       "sync_message_flush" : false,
       "new_partition_numbers" : 6
     } ]
   }

Example Responses
-----------------

None

Status Codes
------------

=========== ===============================
Status Code Description
=========== ===============================
204         The modification is successful.
=========== ===============================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
