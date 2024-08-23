:original_name: ResumeConnectorTask.html

.. _ResumeConnectorTask:

Restarting a Smart Connect Task
===============================

Function
--------

This API is used to restart a Smart Connect task.

URI
---

PUT /v2/{project_id}/instances/{instance_id}/connector/tasks/{task_id}/resume

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

   PUT https://{endpoint}/v2/{project_id}/instances/{instance_id}/connector/tasks/{task_id}/resume

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
