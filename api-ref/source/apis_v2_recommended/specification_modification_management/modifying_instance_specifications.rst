:original_name: ResizeInstance.html

.. _ResizeInstance:

Modifying Instance Specifications
=================================

Function
--------

This API is used to modify instance specifications.

URI
---

POST /v2/{project_id}/instances/{instance_id}/extend

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

   +-------------------+-----------+---------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter         | Mandatory | Type    | Description                                                                                                                                                                |
   +===================+===========+=========+============================================================================================================================================================================+
   | new_spec_code     | No        | String  | Specification ID after the change. If only the disk size is expanded, the specification ID remains unchanged.                                                              |
   +-------------------+-----------+---------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | new_storage_space | No        | Integer | Message storage space in GB after the change. If the bandwidth is expanded, **new_storage_space** cannot be smaller than the minimum disk size specified by the bandwidth. |
   +-------------------+-----------+---------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | oper_type         | No        | String  | Specification modification type. The new specifications support the following types: **horizontal**, **vertical**, **node**, and **storage**.                              |
   +-------------------+-----------+---------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | new_broker_num    | No        | Integer | Number of cluster nodes after the specifications are changed.                                                                                                              |
   +-------------------+-----------+---------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | new_product_id    | No        | String  | Product ID after the specifications are changed. This parameter must be specified for **vertical** expansion (scale-up).                                                   |
   +-------------------+-----------+---------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   ========= ====== ==========================================
   Parameter Type   Description
   ========= ====== ==========================================
   job_id    String ID of the specification modification task.
   ========= ====== ==========================================

Example Requests
----------------

Pay-per-use instance (old specifications)

.. code-block:: text

   POST https://{endpoint}/v2/{project_id}/instances/{instance_id}/extend

   {
     "new_spec_code" : "dms.instance.kafka.cluster.c3.mini",
     "new_storage_space" : 1000
   }

Example Responses
-----------------

**Status code: 200**

Instance specifications are modified successfully.

.. code-block::

   {
     "job_id" : "93b94287-728d-4bb1-a158-cb66cb0854e7"
   }

Status Codes
------------

=========== ==================================================
Status Code Description
=========== ==================================================
200         Instance specifications are modified successfully.
=========== ==================================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
