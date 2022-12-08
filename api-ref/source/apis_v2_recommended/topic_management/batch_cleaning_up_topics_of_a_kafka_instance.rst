:original_name: BatchCleanupInstanceTopic.html

.. _BatchCleanupInstanceTopic:

Batch Cleaning Up Topics of a Kafka Instance
============================================

Function
--------

This API is used to clean up multiple topics of a Kafka instance in batches.

URI
---

POST /v2/kafka/{project_id}/instances/{instance_id}/topics/cleanup

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

   ========= ========= ================ ================================
   Parameter Mandatory Type             Description
   ========= ========= ================ ================================
   topics    No        Array of strings List of topics to be cleared up.
   ========= ========= ================ ================================

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-----------+-----------------------------------------------------------------------------+-------------+
   | Parameter | Type                                                                        | Description |
   +===========+=============================================================================+=============+
   | topics    | Array of :ref:`topics <batchcleanupinstancetopic__response_topics>` objects | Topic list. |
   +-----------+-----------------------------------------------------------------------------+-------------+

.. _batchcleanupinstancetopic__response_topics:

.. table:: **Table 4** topics

   ========= ======= ===================================
   Parameter Type    Description
   ========= ======= ===================================
   id        String  Topic name.
   success   Boolean Whether the cleanup was successful.
   ========= ======= ===================================

Example Requests
----------------

.. code-block:: text

   POST https://{endpoint}/v2/kafka/{project_id}/instances/{instance_id}/topics/cleanup

   {
     "topics" : [ "topic_1", "topic_2" ]
   }

Example Responses
-----------------

**Status code: 200**

The cleanup is successful.

.. code-block::

   {
     "topics" : [ {
       "id" : "topic_1",
       "success" : true
     }, {
       "id" : "topic_2",
       "success" : true
     } ]
   }

Status Codes
------------

=========== ==========================
Status Code Description
=========== ==========================
200         The cleanup is successful.
=========== ==========================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
