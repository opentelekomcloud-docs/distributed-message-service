:original_name: ShowBackgroundTask.html

.. _ShowBackgroundTask:

Querying a Background Task
==========================

Function
--------

This API is used to query a specified background task.

URI
---

GET /v2/{project_id}/instances/{instance_id}/tasks/{task_id}

.. table:: **Table 1** Path Parameters

   =========== ========= ====== ============
   Parameter   Mandatory Type   Description
   =========== ========= ====== ============
   project_id  Yes       String Project ID.
   instance_id Yes       String Instance ID.
   task_id     Yes       String Task ID.
   =========== ========= ====== ============

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameters

   +------------+--------------------------------------------------------------------+------------------+
   | Parameter  | Type                                                               | Description      |
   +============+====================================================================+==================+
   | task_count | String                                                             | Number of tasks. |
   +------------+--------------------------------------------------------------------+------------------+
   | tasks      | Array of :ref:`tasks <showbackgroundtask__response_tasks>` objects | Task list.       |
   +------------+--------------------------------------------------------------------+------------------+

.. _showbackgroundtask__response_tasks:

.. table:: **Table 3** tasks

   ========== ====== ================
   Parameter  Type   Description
   ========== ====== ================
   id         String Task ID.
   name       String Task name.
   user_name  String Username.
   user_id    String User ID.
   params     String Task parameters.
   status     String Task status.
   created_at String Start time.
   updated_at String End time.
   ========== ====== ================

Example Requests
----------------

.. code-block:: text

   GET https://{endpoint}/v2/{project_id}/instances/{instance_id}/tasks/{task_id}

Example Responses
-----------------

**Status code: 200**

The query is successful.

.. code-block::

   {
     "task_count" : "1",
     "tasks" : [ {
       "id" : "8abfa7b272adc5b40172b73130065ae7",
       "name" : "bindInstancePublicIp",
       "user_name" : "paas_dms",
       "user_id" : "3df5acbc24a54fadb62a043c9000a307",
       "params" : "{\"public_ip_id\":\"1aea7aed-e7d8-40ea-b3de-6f3ee9d5db9f\",\"public_ip_address\":\"100.93.2.18\",\"enable_public_ip\":true}",
       "status" : "SUCCESS",
       "created_at" : "2020-06-15T08:55:53.606Z",
       "updated_at" : "2020-06-15T08:55:56.600Z"
     } ]
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
