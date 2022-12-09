:original_name: BatchDeleteInstanceTopic.html

.. _BatchDeleteInstanceTopic:

Batch Deleting Topics of a Kafka Instance
=========================================

Function
--------

This API is used to delete multiple topics of a Kafka instance in batches. If some consumer groups are deleted successfully while some fail to be deleted, a success response is returned with information about consumer groups that fail to be deleted.

URI
---

POST /v2/{project_id}/instances/{instance_id}/topics/delete

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

   ========= ========= ================ =========================
   Parameter Mandatory Type             Description
   ========= ========= ================ =========================
   topics    No        Array of strings List of topics to delete.
   ========= ========= ================ =========================

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-----------+----------------------------------------------------------------------------+-------------+
   | Parameter | Type                                                                       | Description |
   +===========+============================================================================+=============+
   | topics    | Array of :ref:`topics <batchdeleteinstancetopic__response_topics>` objects | Topic list. |
   +-----------+----------------------------------------------------------------------------+-------------+

.. _batchdeleteinstancetopic__response_topics:

.. table:: **Table 4** topics

   ========= ======= ===============================
   Parameter Type    Description
   ========= ======= ===============================
   id        String  Topic name.
   success   Boolean Whether the topics are deleted.
   ========= ======= ===============================

Example Requests
----------------

.. code-block:: text

   POST https://{endpoint}/v2/{project_id}/instances/{instance_id}/topics/delete

   {
     "topics" : [ "topic01" ]
   }

Example Responses
-----------------

**Status code: 200**

The deletion is successful.

.. code-block::

   {
     "topics" : [ {
       "id" : "haha",
       "success" : true
     }, {
       "id" : "aabb",
       "success" : true
     } ]
   }

Status Codes
------------

=========== ===========================
Status Code Description
=========== ===========================
200         The deletion is successful.
=========== ===========================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
