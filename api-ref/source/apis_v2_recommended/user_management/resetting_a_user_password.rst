:original_name: ResetUserPasswrod.html

.. _ResetUserPasswrod:

Resetting a User Password
=========================

Function
--------

This API is used to reset a user password.

URI
---

PUT /v2/{project_id}/instances/{instance_id}/users/{user_name}

.. table:: **Table 1** Path Parameters

   =========== ========= ====== ============
   Parameter   Mandatory Type   Description
   =========== ========= ====== ============
   project_id  Yes       String Project ID.
   instance_id Yes       String Instance ID.
   user_name   Yes       String Username.
   =========== ========= ====== ============

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   ============ ========= ====== =============
   Parameter    Mandatory Type   Description
   ============ ========= ====== =============
   new_password No        String New password.
   ============ ========= ====== =============

Response Parameters
-------------------

None

Example Requests
----------------

Resetting a user password.

.. code-block:: text

   PUT https://{endpoint}/v2/{project_id}/instances/{instance_id}/users/{user_name}

   {
     "new_password" : "Cloud@123"
   }

Example Responses
-----------------

None

Status Codes
------------

=========== ============================
Status Code Description
=========== ============================
204         Password reset successfully.
=========== ============================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
