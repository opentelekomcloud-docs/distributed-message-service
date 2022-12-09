:original_name: BatchDeleteInstanceUsers.html

.. _BatchDeleteInstanceUsers:

Deleting Users in Batches
=========================

Function
--------

This API is used to delete multiple users of a Kafka instance.

URI
---

PUT /v2/{project_id}/instances/{instance_id}/users

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

   +-----------+-----------+------------------+---------------------------------------------------------+
   | Parameter | Mandatory | Type             | Description                                             |
   +===========+===========+==================+=========================================================+
   | action    | No        | String           | Deletion type. Currently, only **delete** is supported. |
   +-----------+-----------+------------------+---------------------------------------------------------+
   | users     | No        | Array of strings | User list.                                              |
   +-----------+-----------+------------------+---------------------------------------------------------+

Response Parameters
-------------------

None

Example Requests
----------------

Deleting users in batches.

.. code-block:: text

   PUT https://{endpoint}/v2/{project_id}/instances/{instance_id}/users

   {
     "action" : "delete",
     "users" : [ "testuser" ]
   }

Example Responses
-----------------

None

Status Codes
------------

=========== ===========================
Status Code Description
=========== ===========================
204         The deletion is successful.
=========== ===========================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
