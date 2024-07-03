:original_name: UpdateInstance.html

.. _UpdateInstance:

Modifying Instance Information
==============================

Function
--------

This API is used to modify the instance information.

URI
---

PUT /v2/{project_id}/instances/{instance_id}

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

   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Mandatory       | Type            | Description                                                                                                                                                                                                              |
   +=======================+=================+=================+==========================================================================================================================================================================================================================+
   | name                  | No              | String          | Instance name.                                                                                                                                                                                                           |
   |                       |                 |                 |                                                                                                                                                                                                                          |
   |                       |                 |                 | An instance name starts with a letter, consists of 4 to 64 characters, and can contain only letters, digits, underscores (_), and hyphens (-).                                                                           |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | description           | No              | String          | Instance description.                                                                                                                                                                                                    |
   |                       |                 |                 |                                                                                                                                                                                                                          |
   |                       |                 |                 | The description can contain a maximum of 1024 characters.                                                                                                                                                                |
   |                       |                 |                 |                                                                                                                                                                                                                          |
   |                       |                 |                 | .. note::                                                                                                                                                                                                                |
   |                       |                 |                 |                                                                                                                                                                                                                          |
   |                       |                 |                 |    The backslash () and quotation mark (") are special characters for JSON messages. When using these characters in a parameter value, add the escape character () before the characters, for example, **\\** and **"**. |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | maintain_begin        | No              | String          | Time at which the maintenance window starts. The format is HH:mm:ss.                                                                                                                                                     |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | maintain_end          | No              | String          | Time at which the maintenance window ends. The format is HH:mm:ss.                                                                                                                                                       |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | security_group_id     | No              | String          | Security group ID.                                                                                                                                                                                                       |
   |                       |                 |                 |                                                                                                                                                                                                                          |
   |                       |                 |                 | To obtain it, log in to the VPC console and view the security group ID on the security group details page.                                                                                                               |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | retention_policy      | No              | String          | Capacity threshold policy.                                                                                                                                                                                               |
   |                       |                 |                 |                                                                                                                                                                                                                          |
   |                       |                 |                 | Options:                                                                                                                                                                                                                 |
   |                       |                 |                 |                                                                                                                                                                                                                          |
   |                       |                 |                 | -  **produce_reject**: New messages cannot be created.                                                                                                                                                                   |
   |                       |                 |                 |                                                                                                                                                                                                                          |
   |                       |                 |                 | -  **time_base**: The earliest messages are deleted.                                                                                                                                                                     |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | enterprise_project_id | No              | String          | Enterprise project.                                                                                                                                                                                                      |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

None

Example Requests
----------------

-  Modifying the name and description of an instance.

   .. code-block:: text

      PUT https://{endpoint}/v2/{project_id}/instances/{instance_id}

      {
        "name" : "kafka001",
        "description" : "kafka description"
      }

-  Modifying the name, description, and maintenance time window of an instance.

   .. code-block:: text

      PUT https://{endpoint}/v2/{project_id}/instances/{instance_id}

      {
        "name" : "dms002",
        "description" : "instance description",
        "maintain_begin" : "02:00:00",
        "maintain_end" : "06:00:00"
      }

-  Changing the capacity threshold policy.

   .. code-block:: text

      PUT https://{endpoint}/v2/{project_id}/instances/{instance_id}

      {
        "retention_policy" : "time_base"
      }

Example Responses
-----------------

None

Status Codes
------------

=========== ==================================================
Status Code Description
=========== ==================================================
204         The instance information is modified successfully.
=========== ==================================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
