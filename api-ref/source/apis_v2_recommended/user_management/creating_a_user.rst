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

   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                                               |
   +=============+===========+========+===========================================================================================================+
   | project_id  | Yes       | String | Project ID. For details about how to obtain it, see :ref:`Obtaining a Project ID <kafka-api-0036212547>`. |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                                              |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                  |
   +=================+=================+=================+==============================================================================================================================+
   | user_name       | No              | String          | Username.                                                                                                                    |
   |                 |                 |                 |                                                                                                                              |
   |                 |                 |                 | This parameter is mandatory for creating a user.                                                                             |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------+
   | user_desc       | No              | String          | User description.                                                                                                            |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------+
   | user_passwd     | No              | String          | Password.                                                                                                                    |
   |                 |                 |                 |                                                                                                                              |
   |                 |                 |                 | This parameter is mandatory for creating a user.                                                                             |
   |                 |                 |                 |                                                                                                                              |
   |                 |                 |                 | The password must be different from the username.                                                                            |
   |                 |                 |                 |                                                                                                                              |
   |                 |                 |                 | The password must meet the following complexity requirements:                                                                |
   |                 |                 |                 |                                                                                                                              |
   |                 |                 |                 | -  Can contain 8 to 32 characters.                                                                                           |
   |                 |                 |                 |                                                                                                                              |
   |                 |                 |                 | -  Must contain at least three of the following character types:                                                             |
   |                 |                 |                 |                                                                                                                              |
   |                 |                 |                 |    -  Lowercase letters                                                                                                      |
   |                 |                 |                 |                                                                                                                              |
   |                 |                 |                 |    -  Uppercase letters                                                                                                      |
   |                 |                 |                 |                                                                                                                              |
   |                 |                 |                 |    -  Digits                                                                                                                 |
   |                 |                 |                 |                                                                                                                              |
   |                 |                 |                 |    -  Special characters include :literal:`\`~!@#$ %^&*()-_=+|[{}]:'",<.>/?` and spaces, and cannot start with a hyphen (-). |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------+

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

Creating a user whose username is test and password is Cxxx3

.. code-block:: text

   POST https://{endpoint}/v2/{project_id}/instances/{instance_id}/users

   {
     "user_name" : "test",
     "user_passwd" : "Cxxx3"
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
