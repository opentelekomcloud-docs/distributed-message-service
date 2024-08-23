:original_name: RestartConnectorTask.html

.. _RestartConnectorTask:

Starting a Smart Connect Task or Restarting a Paused or Running Smart Connect Task
==================================================================================

Function
--------

This API is used to **start a Smart Connect task** or **restart a paused or running Smart Connect task**. Note that the sync progress will reset and the task will restart.

URI
---

PUT /v2/{project_id}/kafka/instances/{instance_id}/connector/tasks/{task_id}/restart

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                        |
   +=============+===========+========+====================================================================================+
   | project_id  | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <kafka-api-0036212547>`. |
   +-------------+-----------+--------+------------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                       |
   +-------------+-----------+--------+------------------------------------------------------------------------------------+
   | task_id     | Yes       | String | Smart Connect task ID.                                                             |
   +-------------+-----------+--------+------------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

None

Example Requests
----------------

.. code-block:: text

   PUT https://{endpoint}/v2/{project_id}/kafka/instances/{instance_id}/connector/tasks/{task_id}/restart

Example Responses
-----------------

None

Status Codes
------------

=========== ===========
Status Code Description
=========== ===========
204         Successful.
=========== ===========

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
