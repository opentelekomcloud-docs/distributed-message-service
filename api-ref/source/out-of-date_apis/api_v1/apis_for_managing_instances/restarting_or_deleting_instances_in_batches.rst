:original_name: kafka-api-180514006.html

.. _kafka-api-180514006:

Restarting or Deleting Instances in Batches
===========================================

.. note::

   This API is out-of-date and may not be maintained in the future. Please use the API described in :ref:`Batch Restarting or Deleting Instances <batchrestartordeleteinstances>`.

Function
--------

This API is used to restart or delete instances in batches.

When an instance is being restarted, message retrieval and creation requests of the client will be rejected.

Deleting an instance will delete the data in the instance without any backup. Exercise caution when performing this operation.

URI
---

POST /v1.0/{project_id}/instances/action

:ref:`Table 1 <kafka-api-180514006__en-us_topic_0128036898_table98991536279>` describes the parameters.

.. _kafka-api-180514006__en-us_topic_0128036898_table98991536279:

.. table:: **Table 1** Parameters

   ========== ====== ========= ==============================
   Parameter  Type   Mandatory Description
   ========== ====== ========= ==============================
   project_id String Yes       Indicates the ID of a project.
   ========== ====== ========= ==============================

Request
-------

**Request parameters**

:ref:`Table 2 <kafka-api-180514006__en-us_topic_0128036898_table890715392717>` describes the parameters.

.. _kafka-api-180514006__en-us_topic_0128036898_table890715392717:

.. table:: **Table 2** Request parameters

   +------------+--------+-----------+---------------------------------------------------------------------------------------------------------------------+
   | Parameter  | Type   | Mandatory | Description                                                                                                         |
   +============+========+===========+=====================================================================================================================+
   | action     | String | Yes       | Indicates the operation to be performed on instances. The value of this parameter can be **restart** or **delete**. |
   +------------+--------+-----------+---------------------------------------------------------------------------------------------------------------------+
   | instances  | Array  | No        | Indicates the list of instance IDs.                                                                                 |
   +------------+--------+-----------+---------------------------------------------------------------------------------------------------------------------+
   | allFailure | String | No        | When set to **kafka**, indicates all Kafka instances that fail to be created are to be deleted.                     |
   +------------+--------+-----------+---------------------------------------------------------------------------------------------------------------------+

**Example request**

Restarting instances in batches:

.. code-block:: text

   POST https://{dms_endpoint}/v1.0/{project_id}/instances/action
   {
       "action" : "restart",
       "instances" : ["54602a9d-5e22-4239-9123-77e350df4a34", "7166cdea-dbad-4d79-9610-7163e6f8b640"]
   }

Deleting instances in batches:

.. code-block:: text

   POST https://{dms_endpoint}/v1.0/{project_id}/instances/action
   {
       "action" : "delete",
       "instances" : ["54602a9d-5e22-4239-9123-77e350df4a34", "7166cdea-dbad-4d79-9610-7163e6f8b640"]
   }

Deleting all instances that fail to be created:

.. code-block:: text

   POST https://{dms_endpoint}/v1.0/{project_id}/instances/action
   {
       "action" : "delete",
       "allFailure" : "kafka"
   }

Response
--------

**Response parameters**

When **action** is set to **delete**, **allFailure** is set to **kafka**, and an empty response is returned, the instances are deleted successfully. :ref:`Table 3 <kafka-api-180514006__en-us_topic_0128036898_table189241953152710>` describes the parameters.

.. _kafka-api-180514006__en-us_topic_0128036898_table189241953152710:

.. table:: **Table 3** Response parameters

   ========= ===== ==============================================
   Parameter Type  Description
   ========= ===== ==============================================
   results   Array Indicates the result of instance modification.
   ========= ===== ==============================================

.. table:: **Table 4** results parameter description

   +-----------+--------+-----------------------------------------------------------------------+
   | Parameter | Type   | Description                                                           |
   +===========+========+=======================================================================+
   | instance  | String | Indicates the instance ID.                                            |
   +-----------+--------+-----------------------------------------------------------------------+
   | result    | String | Indicates an operation result, which can be **success** or **failed** |
   +-----------+--------+-----------------------------------------------------------------------+

**Example response**

.. code-block::

   {
       "results": [
           {
               "result": "success",
               "instance": "afc90a2a-a02c-4cba-94d5-58dfa9ad1e0d"
           },
           {
               "result": "success",
               "instance": "67fc5f8d-3986-4f02-bb75-4075a23112de"
           }
       ]
   }

Status Code
-----------

:ref:`Table 5 <kafka-api-180514006__en-us_topic_0128036898_table17944125315273>` describes the status code of successful operations. For details about other status codes, see :ref:`Status Code <kafka-api-0034672261>`.

.. _kafka-api-180514006__en-us_topic_0128036898_table17944125315273:

.. table:: **Table 5** Status code

   =========== =======================================================
   Status Code Description
   =========== =======================================================
   200         The instances are restarted or deleted successfully.
   204         Successfully deleting an instance failed to be created.
   =========== =======================================================
