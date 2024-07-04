:original_name: ShowTopicAccessPolicy.html

.. _ShowTopicAccessPolicy:

Querying User Permissions
=========================

Function
--------

This API is used to query user permissions.

User management is supported only when SASL is enabled for the Kafka instance.

URI
---

GET /v1/{project_id}/instances/{instance_id}/topics/{topic_name}/accesspolicy

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                                               |
   +=============+===========+========+===========================================================================================================+
   | project_id  | Yes       | String | Project ID. For details about how to obtain it, see :ref:`Obtaining a Project ID <kafka-api-0036212547>`. |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                                              |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | topic_name  | Yes       | String | Topic name.                                                                                               |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameters

   +-----------------------+-------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                                                | Description                                                                                                                                     |
   +=======================+=====================================================================================+=================================================================================================================================================+
   | name                  | String                                                                              | Consumer group description.                                                                                                                     |
   +-----------------------+-------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | topic_type            | Integer                                                                             | Specified IPv4 private IP addresses.                                                                                                            |
   |                       |                                                                                     |                                                                                                                                                 |
   |                       |                                                                                     | The number of specified IP addresses must be less than or equal to the number of new brokers.                                                   |
   |                       |                                                                                     |                                                                                                                                                 |
   |                       |                                                                                     | If the number of specified IP addresses is less than the number of brokers, the unspecified brokers are randomly assigned private IP addresses. |
   +-----------------------+-------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | policies              | Array of :ref:`PolicyEntity <showtopicaccesspolicy__response_policyentity>` objects | New brokers use the standby subnet ID in instance expansion.                                                                                    |
   |                       |                                                                                     |                                                                                                                                                 |
   |                       |                                                                                     | This value is transferred when a standby subnet is used in instance expansion.                                                                  |
   |                       |                                                                                     |                                                                                                                                                 |
   |                       |                                                                                     | Contact customer service to use the value.                                                                                                      |
   +-----------------------+-------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+

.. _showtopicaccesspolicy__response_policyentity:

.. table:: **Table 3** PolicyEntity

   +-----------------------+-----------------------+-------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                 |
   +=======================+=======================+=============================================================+
   | owner                 | Boolean               | Whether the user is the one selected during topic creation. |
   +-----------------------+-----------------------+-------------------------------------------------------------+
   | user_name             | String                | Username.                                                   |
   +-----------------------+-----------------------+-------------------------------------------------------------+
   | access_policy         | String                | Permission type.                                            |
   |                       |                       |                                                             |
   |                       |                       | -  **all**: publish and subscribe permissions.              |
   |                       |                       |                                                             |
   |                       |                       | -  **pub**: publish permissions.                            |
   |                       |                       |                                                             |
   |                       |                       | -  **sub**: subscribe permissions.                          |
   +-----------------------+-----------------------+-------------------------------------------------------------+

Example Requests
----------------

Querying user permissions for a topic.

.. code-block:: text

   GET https://{endpoint}/v1/{project_id}/instances/{instance_id}/topics/{topic_name}/accesspolicy

Example Responses
-----------------

**Status code: 200**

The query is successful.

.. code-block::

   {
     "name" : "topic-test",
     "policies" : [ {
       "owner" : false,
       "user_name" : "xxxa",
       "access_policy" : "pub"
     }, {
       "owner" : false,
       "user_name" : "root",
       "access_policy" : "all"
     } ],
     "topic_type" : 0
   }

Status Codes
------------

=========== ========================
Status Code Description
=========== ========================
200         The query is successful.
=========== ========================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
