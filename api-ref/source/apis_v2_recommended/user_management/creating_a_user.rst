:original_name: CreateInstanceUser.html

.. _CreateInstanceUser:

Creating a User
===============

Function
--------

This API is used to create a user for a Kafka instance for which SASL is enabled.

URI
---

POST /v2/{project_id}/instances/{instance_id}/users

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
   | user_name       | No              | String          | Username.                                                                                                       |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------+
   | user_passwd     | No              | String          | User password.                                                                                                  |
   |                 |                 |                 |                                                                                                                 |
   |                 |                 |                 | The password must be different from the username. The password must meet the following complexity requirements: |
   |                 |                 |                 |                                                                                                                 |
   |                 |                 |                 | -  Contains 8 to 32 characters.                                                                                 |
   |                 |                 |                 |                                                                                                                 |
   |                 |                 |                 | -  Contains at least two of the following character types:                                                      |
   |                 |                 |                 |                                                                                                                 |
   |                 |                 |                 |    -  Lowercase letters                                                                                         |
   |                 |                 |                 |                                                                                                                 |
   |                 |                 |                 |    -  Uppercase letters                                                                                         |
   |                 |                 |                 |                                                                                                                 |
   |                 |                 |                 |    -  Digits                                                                                                    |
   |                 |                 |                 |                                                                                                                 |
   |                 |                 |                 |    -  Special characters :literal:`\`~!@#$%^&*()-_=+|[{}]:'"",<.>/?`                                            |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 400**

.. table:: **Table 3** Response body parameters

   ========== ====== ==================
   Parameter  Type   Description
   ========== ====== ==================
   error_code String Error code.
   error_msg  String Error description.
   ========== ====== ==================

**Status code: 403**

.. table:: **Table 4** Response body parameters

   ========== ====== ==================
   Parameter  Type   Description
   ========== ====== ==================
   error_code String Error code.
   error_msg  String Error description.
   ========== ====== ==================

Example Requests
----------------

Creating a user.

.. code-block:: text

   POST https://{endpoint}/v2/{project_id}/instances/{instance_id}/users

   {
     "user_name" : "test",
     "user_passwd" : "Cloud@123"
   }

Example Responses
-----------------

None

Status Codes
------------

=========== ===========================
Status Code Description
=========== ===========================
204         The creation is successful.
400         Invalid parameters.
403         Authentication failed.
=========== ===========================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
