:original_name: UpdateTopicAccessPolicy.html

.. _UpdateTopicAccessPolicy:

Granting User Permissions
=========================

Function
--------

This API is used to grant user permissions.

User management is supported only when SASL is enabled for the Kafka instance.

URI
---

POST /v1/{project_id}/instances/{instance_id}/topics/accesspolicy

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

   +-----------+-----------+------------------------------------------------------------------------------------------------------------+-------------+
   | Parameter | Mandatory | Type                                                                                                       | Description |
   +===========+===========+============================================================================================================+=============+
   | topics    | Yes       | Array of :ref:`AccessPolicyTopicEntity <updatetopicaccesspolicy__request_accesspolicytopicentity>` objects | Topic list. |
   +-----------+-----------+------------------------------------------------------------------------------------------------------------+-------------+

.. _updatetopicaccesspolicy__request_accesspolicytopicentity:

.. table:: **Table 3** AccessPolicyTopicEntity

   +-----------+-----------+--------------------------------------------------------------------------------------------------+------------------+
   | Parameter | Mandatory | Type                                                                                             | Description      |
   +===========+===========+==================================================================================================+==================+
   | name      | Yes       | String                                                                                           | Topic name.      |
   +-----------+-----------+--------------------------------------------------------------------------------------------------+------------------+
   | policies  | Yes       | Array of :ref:`AccessPolicyEntity <updatetopicaccesspolicy__request_accesspolicyentity>` objects | Permission list. |
   +-----------+-----------+--------------------------------------------------------------------------------------------------+------------------+

.. _updatetopicaccesspolicy__request_accesspolicyentity:

.. table:: **Table 4** AccessPolicyEntity

   +-----------------+-----------------+-----------------+------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                |
   +=================+=================+=================+============================================================+
   | user_name       | No              | String          | Username.                                                  |
   |                 |                 |                 |                                                            |
   |                 |                 |                 | This parameter is mandatory when you set user permissions. |
   +-----------------+-----------------+-----------------+------------------------------------------------------------+
   | access_policy   | No              | String          | Permission type.                                           |
   |                 |                 |                 |                                                            |
   |                 |                 |                 | -  **all**: publish and subscribe permissions.             |
   |                 |                 |                 |                                                            |
   |                 |                 |                 | -  **pub**: publish permissions.                           |
   |                 |                 |                 |                                                            |
   |                 |                 |                 | -  **sub**: subscribe permissions.                         |
   |                 |                 |                 |                                                            |
   |                 |                 |                 | This parameter is mandatory when you set user permissions. |
   +-----------------+-----------------+-----------------+------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 400**

.. table:: **Table 5** Response body parameters

   ========== ====== ==================
   Parameter  Type   Description
   ========== ====== ==================
   error_code String Error code.
   error_msg  String Error description.
   ========== ====== ==================

**Status code: 403**

.. table:: **Table 6** Response body parameters

   ========== ====== ==================
   Parameter  Type   Description
   ========== ====== ==================
   error_code String Error code.
   error_msg  String Error description.
   ========== ====== ==================

Example Requests
----------------

Granting the root user the permission to publish and subscribe to topic-test

.. code-block:: text

   POST https://{endpoint}/v1/{project_id}/instances/{instance_id}/topics/accesspolicy

   {
     "topics" : [ {
       "name" : "topic-test",
       "policies" : [ {
         "user_name" : "root",
         "access_policy" : "all"
       } ]
     } ]
   }

Example Responses
-----------------

None

Status Codes
------------

=========== =========================
Status Code Description
=========== =========================
204         The update is successful.
400         Invalid parameters.
403         Authentication failed.
=========== =========================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
