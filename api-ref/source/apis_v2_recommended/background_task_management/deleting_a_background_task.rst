:original_name: DeleteBackgroundTask.html

.. _DeleteBackgroundTask:

Deleting a Background Task
==========================

Function
--------

This API is used to delete a specified background task.

URI
---

DELETE /v2/{project_id}/instances/{instance_id}/tasks/{task_id}

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                                               |
   +=============+===========+========+===========================================================================================================+
   | project_id  | Yes       | String | Project ID. For details about how to obtain it, see :ref:`Obtaining a Project ID <kafka-api-0036212547>`. |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                                              |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | task_id     | Yes       | String | Task ID.                                                                                                  |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

None

Example Requests
----------------

Deleting a specified background task

.. code-block:: text

   DELETE https://{endpoint}/v2/{project_id}/instances/{instance_id}/tasks/{task_id}

Example Responses
-----------------

None

Status Codes
------------

=========== ============================================
Status Code Description
=========== ============================================
204         The background task is deleted successfully.
=========== ============================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
