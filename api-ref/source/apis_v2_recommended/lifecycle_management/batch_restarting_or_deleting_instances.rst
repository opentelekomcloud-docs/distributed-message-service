:original_name: BatchRestartOrDeleteInstances.html

.. _BatchRestartOrDeleteInstances:

Batch Restarting or Deleting Instances
======================================

Function
--------

This API is used to restart or delete instances in batches.

When an instance is being restarted, message retrieval and creation requests of the client will be rejected.

Deleting an instance will delete the data in the instance without any backup. Exercise caution when performing this operation.

URI
---

POST /v2/{project_id}/instances/action

.. table:: **Table 1** Path Parameters

   ========== ========= ====== ===========
   Parameter  Mandatory Type   Description
   ========== ========= ====== ===========
   project_id Yes       String Project ID.
   ========== ========= ====== ===========

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   +-------------+-----------+------------------+------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type             | Description                                                                              |
   +=============+===========+==================+==========================================================================================+
   | instances   | No        | Array of strings | List of instance IDs.                                                                    |
   +-------------+-----------+------------------+------------------------------------------------------------------------------------------+
   | action      | Yes       | String           | Operation to be performed on instances. The value can be **restart** or **delete**.      |
   +-------------+-----------+------------------+------------------------------------------------------------------------------------------+
   | all_failure | No        | String           | Value **kafka** indicates all Kafka instances that fail to be created are to be deleted. |
   +-------------+-----------+------------------+------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-----------+-----------------------------------------------------------------------------------+----------------------------------+
   | Parameter | Type                                                                              | Description                      |
   +===========+===================================================================================+==================================+
   | results   | Array of :ref:`results <batchrestartordeleteinstances__response_results>` objects | Result of instance modification. |
   +-----------+-----------------------------------------------------------------------------------+----------------------------------+

.. _batchrestartordeleteinstances__response_results:

.. table:: **Table 4** results

   +-----------------------+-----------------------+------------------------------------------+
   | Parameter             | Type                  | Description                              |
   +=======================+=======================+==========================================+
   | result                | String                | Operation result.                        |
   |                       |                       |                                          |
   |                       |                       | -  **success**: The operation succeeded. |
   |                       |                       |                                          |
   |                       |                       | -  **failed**: The operation failed.     |
   +-----------------------+-----------------------+------------------------------------------+
   | instance              | String                | Instance ID.                             |
   +-----------------------+-----------------------+------------------------------------------+

Example Requests
----------------

-  Restarting instances in batches.

   .. code-block:: text

      POST https://{endpoint}/v2/{project_id}/instances/action

      {
        "action" : "restart",
        "instances" : [ "54602a9d-5e22-4239-9123-77e350df4a34", "7166cdea-dbad-4d79-9610-7163e6f8b640" ]
      }

-  Deleting instances in batches.

   .. code-block:: text

      POST https://{endpoint}/v2/{project_id}/instances/action

      {
        "action" : "delete",
        "instances" : [ "54602a9d-5e22-4239-9123-77e350df4a34", "7166cdea-dbad-4d79-9610-7163e6f8b640" ]
      }

-  Deleting all instances that fail to be created.

   .. code-block:: text

      POST https://{endpoint}/v2/{project_id}/instances/action

      {
        "action" : "delete",
        "all_failure" : "kafka"
      }

Example Responses
-----------------

**Status code: 200**

The instances are restarted or deleted successfully.

.. code-block::

   {
     "results" : [ {
       "result" : "success",
       "instance" : "019cacb7-4ff0-4d3c-9f33-f5f7b7fdc0e6"
     } ]
   }

Status Codes
------------

=========== ====================================================
Status Code Description
=========== ====================================================
200         The instances are restarted or deleted successfully.
=========== ====================================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
