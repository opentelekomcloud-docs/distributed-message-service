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

   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                                               |
   +=============+===========+========+===========================================================================================================+
   | project_id  | Yes       | String | Project ID. For details about how to obtain it, see :ref:`Obtaining a Project ID <kafka-api-0036212547>`. |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                                              |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | user_name   | Yes       | String | Username.                                                                                                 |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                    |
   +=================+=================+=================+================================================================================================================================+
   | new_password    | No              | String          | New password.                                                                                                                  |
   |                 |                 |                 |                                                                                                                                |
   |                 |                 |                 | This parameter is mandatory for resetting a user password.                                                                     |
   |                 |                 |                 |                                                                                                                                |
   |                 |                 |                 | It cannot be the username or the username spelled backwards. The password must meet the following complexity requirements:     |
   |                 |                 |                 |                                                                                                                                |
   |                 |                 |                 | -  Can contain 8 to 32 characters.                                                                                             |
   |                 |                 |                 |                                                                                                                                |
   |                 |                 |                 | -  Must contain at least three of the following character types:                                                               |
   |                 |                 |                 |                                                                                                                                |
   |                 |                 |                 |    -  Lowercase letters                                                                                                        |
   |                 |                 |                 |                                                                                                                                |
   |                 |                 |                 |    -  Uppercase letters                                                                                                        |
   |                 |                 |                 |                                                                                                                                |
   |                 |                 |                 |    -  Digits                                                                                                                   |
   |                 |                 |                 |                                                                                                                                |
   |                 |                 |                 |    -  Special characters include (:literal:`\`~!@#$ %^&*()-_=+|[{}]:'",<.>/?`) and spaces, and cannot start with a hyphen (-). |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

None

Example Requests
----------------

Resetting a user password.

.. code-block:: text

   PUT https://{endpoint}/v2/{project_id}/instances/{instance_id}/users/{user_name}

   {
     "new_password" : "Cxxx3"
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
