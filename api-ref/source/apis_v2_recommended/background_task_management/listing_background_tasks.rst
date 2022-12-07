:original_name: ListBackgroundTasks.html

.. _ListBackgroundTasks:

Listing Background Tasks
========================

Function
--------

This API is used to list background tasks of an instance.

URI
---

GET /v2/{project_id}/instances/{instance_id}/tasks

.. table:: **Table 1** Path Parameters

   =========== ========= ====== ============
   Parameter   Mandatory Type   Description
   =========== ========= ====== ============
   project_id  Yes       String Project ID.
   instance_id Yes       String Instance ID.
   =========== ========= ====== ============

.. table:: **Table 2** Query Parameters

   +------------+-----------+---------+--------------------------------------------------------------------+
   | Parameter  | Mandatory | Type    | Description                                                        |
   +============+===========+=========+====================================================================+
   | start      | No        | Integer | ID of the task where the query starts.                             |
   +------------+-----------+---------+--------------------------------------------------------------------+
   | limit      | No        | Integer | Number of tasks to be queried.                                     |
   +------------+-----------+---------+--------------------------------------------------------------------+
   | begin_time | No        | String  | Time of task where the query starts. The format is YYYYMMDDHHmmss. |
   +------------+-----------+---------+--------------------------------------------------------------------+
   | end_time   | No        | String  | Time of task where the query ends. The format is YYYYMMDDHHmmss.   |
   +------------+-----------+---------+--------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +------------+---------------------------------------------------------------------+------------------+
   | Parameter  | Type                                                                | Description      |
   +============+=====================================================================+==================+
   | task_count | String                                                              | Number of tasks. |
   +------------+---------------------------------------------------------------------+------------------+
   | tasks      | Array of :ref:`tasks <listbackgroundtasks__response_tasks>` objects | Task list.       |
   +------------+---------------------------------------------------------------------+------------------+

.. _listbackgroundtasks__response_tasks:

.. table:: **Table 4** tasks

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

.. code-block::

   'GET https://{endpoint}/v2/{project_id}/instances/{instance_id}/tasks?start={start}&limit={limit}&begin_time={begin_time}&end_time={end_time}'

Example Responses
-----------------

**Status code: 200**

Background tasks are listed successfully.

.. code-block::

   {
     "task_count" : "4",
     "tasks" : [ {
       "id" : "8abfa7b372160bfd0172165864064079",
       "name" : "modifyAutoTopic",
       "user_name" : "paas_dms",
       "user_id" : "3df5acbc24a54fadb62a043c9000a307",
       "params" : "{\"old_auto_status\":true,\"new_auto_status\":false}",
       "status" : "EXECUTING",
       "created_at" : "2020-05-15T03:19:51.046Z",
       "updated_at" : "2020-05-15T03:19:51.065Z"
     }, {
       "id" : "8abfa7b372160bfd017216560af83e6e",
       "name" : "changeRetentionPolicy",
       "user_name" : "paas_dms",
       "user_id" : "3df5acbc24a54fadb62a043c9000a307",
       "params" : "{\"new_retention_policy\":\"produce_reject\",\"origin_retention_policy\":\"time_base\"}",
       "status" : "SUCCESS",
       "created_at" : "2020-05-15T03:17:17.176Z",
       "updated_at" : "2020-05-15T03:17:22.162Z"
     } ]
   }

Status Codes
------------

=========== =========================================
Status Code Description
=========== =========================================
200         Background tasks are listed successfully.
=========== =========================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
