:original_name: kafka-api-180514004.html

.. _kafka-api-180514004:

Modifying an Instance
=====================

.. note::

   This API is out-of-date and may not be maintained in the future. Please use the API described in :ref:`Modifying Instance Information <updateinstance>`.

Function
--------

This API is used to modify the instance information, including the instance name, description, maintenance window, and security group.

URI
---

PUT /v1.0/{project_id}/instances/{instance_id}

.. table:: **Table 1** Parameters

   =========== ====== ========= ==============================
   Parameter   Type   Mandatory Description
   =========== ====== ========= ==============================
   project_id  String Yes       Indicates the ID of a project.
   instance_id String Yes       Indicates the instance ID.
   =========== ====== ========= ==============================

Request
-------

**Request parameters**

:ref:`Table 2 <kafka-api-180514004__en-us_topic_0128036897_table1535615281916>` describes the parameters.

.. _kafka-api-180514004__en-us_topic_0128036897_table1535615281916:

.. table:: **Table 2** Request parameters

   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type            | Mandatory       | Description                                                                                                                                                                                                                                                                                      |
   +=======================+=================+=================+==================================================================================================================================================================================================================================================================================================+
   | name                  | String          | No              | Indicates the instance name.                                                                                                                                                                                                                                                                     |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                  |
   |                       |                 |                 | An instance name consists of 4 to 64 characters including letters, digits, and hyphens (-) and must start with a letter.                                                                                                                                                                         |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | description           | String          | No              | Indicates the description of an instance.                                                                                                                                                                                                                                                        |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                  |
   |                       |                 |                 | It is a character string containing not more than 1024 characters.                                                                                                                                                                                                                               |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                  |
   |                       |                 |                 | .. note::                                                                                                                                                                                                                                                                                        |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                  |
   |                       |                 |                 |    The backslash (\\) and quotation mark (") are special characters for JSON packets. When using these characters in a parameter value, add the escape character (\\) before these characters, for example, **\\\\** and **\\"**.                                                                |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | maintain_begin        | String          | No              | Indicates the time at which a maintenance time window starts.                                                                                                                                                                                                                                    |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                  |
   |                       |                 |                 | Format: HH:mm:ss                                                                                                                                                                                                                                                                                 |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                  |
   |                       |                 |                 | -  The start time and end time of the maintenance time window must indicate the time segment of a supported maintenance time window. For details about how to query the time segments of supported maintenance time windows, see :ref:`Querying Maintenance Time Windows <kafka-api-180514010>`. |
   |                       |                 |                 | -  The start time must be set to 22:00:00, 02:00:00, 06:00:00, 10:00:00, 14:00:00, or 18:00:00.                                                                                                                                                                                                  |
   |                       |                 |                 | -  Parameters **maintain_begin** and **maintain_end** must be set in pairs. If parameter **maintain_begin** is left blank, parameter **maintain_end** is also left blank. In this case, the system automatically sets the start time to 02:00:00.                                                |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | maintain_end          | String          | No              | Indicates the time at which a maintenance time window ends.                                                                                                                                                                                                                                      |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                  |
   |                       |                 |                 | Format: HH:mm:ss                                                                                                                                                                                                                                                                                 |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                  |
   |                       |                 |                 | -  The start time and end time of the maintenance time window must indicate the time segment of a supported maintenance time window. For details about how to query the time segments of supported maintenance time windows, see :ref:`Querying Maintenance Time Windows <kafka-api-180514010>`. |
   |                       |                 |                 | -  The end time is four hours later than the start time. For example, if the start time is 22:00:00, the end time is 02:00:00.                                                                                                                                                                   |
   |                       |                 |                 | -  Parameters **maintain_begin** and **maintain_end** must be set in pairs. If parameter **maintain_end** is left blank, parameter **maintain_start** is also left blank. In this case, the system automatically sets the end time to 06:00:00.                                                  |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | security_group_id     | String          | No              | Indicates the security group ID.                                                                                                                                                                                                                                                                 |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | retention_policy      | String          | No              | Indicates the capacity threshold policy. Options:                                                                                                                                                                                                                                                |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                  |
   |                       |                 |                 | -  **produce_reject**: New messages cannot be created.                                                                                                                                                                                                                                           |
   |                       |                 |                 | -  **time_base**: The earliest messages are deleted.                                                                                                                                                                                                                                             |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | enterprise_project_id | String          | No              | Indicates the enterprise project ID.                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

**Example request**

Example 1:

.. code-block:: text

   PUT https://{dms_endpoint}/v1.0/{project_id}/instances/{instance_id}
   {
       "name": "dms002",
       "description": "instance description"
   }

Example 2:

.. code-block:: text

   PUT https://{dms_endpoint}/v1.0/{project_id}/instances/{instance_id}
   {
        "name": "dms002",
        "description": "instance description",
        "maintain_begin":"02:00:00",
        "maintain_end":"06:00:00"
   }

Response
--------

**Response parameters**

None.

**Example response**

None.

Status Code
-----------

:ref:`Table 3 <kafka-api-180514004__en-us_topic_0128036897_table044092812115>` describes the status code of successful operations. For details about other status codes, see :ref:`Status Code <kafka-api-0034672261>`.

.. _kafka-api-180514004__en-us_topic_0128036897_table044092812115:

.. table:: **Table 3** Status code

   =========== ======================================
   Status Code Description
   =========== ======================================
   204         The instance is modified successfully.
   =========== ======================================
