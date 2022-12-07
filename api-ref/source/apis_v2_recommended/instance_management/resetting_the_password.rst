:original_name: ResetPassword.html

.. _ResetPassword:

Resetting the Password
======================

Function
--------

This API is used to reset the password.

URI
---

POST /v2/{project_id}/instances/{instance_id}/password

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

   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                     |
   +=================+=================+=================+=================================================================================================================+
   | new_password    | No              | String          | The password can contain 8 to 32 characters, and must contain at least three types of the following characters: |
   |                 |                 |                 |                                                                                                                 |
   |                 |                 |                 | -  Uppercase letters                                                                                            |
   |                 |                 |                 |                                                                                                                 |
   |                 |                 |                 | -  Lowercase letters                                                                                            |
   |                 |                 |                 |                                                                                                                 |
   |                 |                 |                 | -  Digits                                                                                                       |
   |                 |                 |                 |                                                                                                                 |
   |                 |                 |                 | -  Special characters`~!@#$%^&*()-_=+\\|[{}];:'"",<.>/? and spaces, and cannot start with a hyphen (-).         |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

None

Example Requests
----------------

.. code-block:: text

   POST https://{endpoint}/v2/{project_id}/instances/{instance_id}/password

   {
     "new_password" : "********"
   }

Example Responses
-----------------

None

Status Codes
------------

=========== ===================================
Status Code Description
=========== ===================================
204         The password is reset successfully.
=========== ===================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
