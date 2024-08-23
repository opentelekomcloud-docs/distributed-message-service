:original_name: CreateKafkaConsumerGroup.html

.. _CreateKafkaConsumerGroup:

Creating a Consumer Group
=========================

Function
--------

This API is used to create a consumer group.

URI
---

POST /v2/{project_id}/kafka/instances/{instance_id}/group

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

   ========== ========= ====== ===========================
   Parameter  Mandatory Type   Description
   ========== ========= ====== ===========================
   group_name Yes       String Consumer group name.
   group_desc No        String Consumer group description.
   ========== ========= ====== ===========================

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                     |
   +=======================+=======================+=================================================================================================================================================+
   | ``-``                 | String                | Specified IPv4 private IP addresses.                                                                                                            |
   |                       |                       |                                                                                                                                                 |
   |                       |                       | The number of specified IP addresses must be less than or equal to the number of new brokers.                                                   |
   |                       |                       |                                                                                                                                                 |
   |                       |                       | If the number of specified IP addresses is less than the number of brokers, the unspecified brokers are randomly assigned private IP addresses. |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+

**Status code: 400**

.. table:: **Table 4** Response body parameters

   ========== ====== ==================
   Parameter  Type   Description
   ========== ====== ==================
   error_code String Error code.
   error_msg  String Error description.
   ========== ====== ==================

Example Requests
----------------

Creating a consumer group named test

.. code-block:: text

   POST https://{endpoint}/v2/{project_id}/kafka/instances/{instance_id}/group

   {
     "group_name" : "test"
   }

Example Responses
-----------------

**Status code: 200**

Creation succeeded.

.. code-block::

   success

Status Codes
------------

=========== ===================
Status Code Description
=========== ===================
200         Creation succeeded.
400         Creation failed.
=========== ===================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
