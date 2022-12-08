:original_name: BatchDeleteGroup.html

.. _BatchDeleteGroup:

Batch Deleting Consumer Groups of a Kafka Instance
==================================================

Function
--------

This API is used to delete multiple consumer groups of a Kafka instance in batches.

URI
---

POST /v2/{project_id}/instances/{instance_id}/groups/batch-delete

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

   +-----------+-----------+------------------+----------------------------------------+
   | Parameter | Mandatory | Type             | Description                            |
   +===========+===========+==================+========================================+
   | [items]   | Yes       | Array of strings | List of consumer groups to be deleted. |
   +-----------+-----------+------------------+----------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +---------------+----------------------------------------------------------------------------------+----------------------------------------------------+
   | Parameter     | Type                                                                             | Description                                        |
   +===============+==================================================================================+====================================================+
   | failed_groups | Array of :ref:`failed_groups <batchdeletegroup__response_failed_groups>` objects | List of consumer groups that failed to be deleted. |
   +---------------+----------------------------------------------------------------------------------+----------------------------------------------------+
   | total         | Integer                                                                          | Number of records that fail to be deleted.         |
   +---------------+----------------------------------------------------------------------------------+----------------------------------------------------+

.. _batchdeletegroup__response_failed_groups:

.. table:: **Table 4** failed_groups

   ============= ====== ================================================
   Parameter     Type   Description
   ============= ====== ================================================
   group_id      String ID of consumer groups that failed to be deleted.
   error_message String Cause of the deletion failure.
   ============= ====== ================================================

Example Requests
----------------

.. code-block:: text

   POST https://{endpoint}/v2/{project_id}/instances/{instance_id}/groups/batch-delete

   [ "group1", "group2" ]

Example Responses
-----------------

**Status code: 200**

The consumer groups are deleted successfully.

.. code-block::

   {
     "failed_groups" : [ {
       "group_id" : "test-1",
       "error_message" : "UNKNOW"
     }, {
       "group_id" : "test-2",
       "error_message" : "UNKNOW"
     } ],
     "total" : 2
   }

Status Codes
------------

=========== =============================================
Status Code Description
=========== =============================================
200         The consumer groups are deleted successfully.
=========== =============================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
