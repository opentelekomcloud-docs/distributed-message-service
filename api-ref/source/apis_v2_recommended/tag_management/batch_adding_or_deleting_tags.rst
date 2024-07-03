:original_name: BatchCreateOrDeleteKafkaTag.html

.. _BatchCreateOrDeleteKafkaTag:

Batch Adding or Deleting Tags
=============================

Function
--------

This API is used to add or delete instance tags in batches.

URI
---

POST /v2/{project_id}/kafka/{instance_id}/tags/action

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

   +-----------------+-----------------+------------------------------------------------------------------------------------+--------------------------------------------------+
   | Parameter       | Mandatory       | Type                                                                               | Description                                      |
   +=================+=================+====================================================================================+==================================================+
   | action          | No              | String                                                                             | Operation. Only lowercase letters are supported. |
   |                 |                 |                                                                                    |                                                  |
   |                 |                 |                                                                                    | -  **create**: Tags are created.                 |
   |                 |                 |                                                                                    |                                                  |
   |                 |                 |                                                                                    | -  **delete**: Tags are deleted.                 |
   +-----------------+-----------------+------------------------------------------------------------------------------------+--------------------------------------------------+
   | tags            | No              | Array of :ref:`TagEntity <batchcreateordeletekafkatag__request_tagentity>` objects | Tag list.                                        |
   +-----------------+-----------------+------------------------------------------------------------------------------------+--------------------------------------------------+

.. _batchcreateordeletekafkatag__request_tagentity:

.. table:: **Table 3** TagEntity

   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                             |
   +=================+=================+=================+=========================================================================+
   | key             | No              | String          | Tag key, which:                                                         |
   |                 |                 |                 |                                                                         |
   |                 |                 |                 | -  Must be specified.                                                   |
   |                 |                 |                 |                                                                         |
   |                 |                 |                 | -  Must be unique for the same instance.                                |
   |                 |                 |                 |                                                                         |
   |                 |                 |                 | -  Can contain 1 to 128 characters.                                     |
   |                 |                 |                 |                                                                         |
   |                 |                 |                 | -  Can contain letters, digits, spaces, and special characters \_.:=+-@ |
   |                 |                 |                 |                                                                         |
   |                 |                 |                 | -  Cannot start or end with a space.                                    |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------+
   | value           | No              | String          | Tag value.                                                              |
   |                 |                 |                 |                                                                         |
   |                 |                 |                 | -  Can contain 0 to 255 characters.                                     |
   |                 |                 |                 |                                                                         |
   |                 |                 |                 | -  Can contain letters, digits, spaces, and special characters \_.:=+-@ |
   |                 |                 |                 |                                                                         |
   |                 |                 |                 | -  Cannot start or end with a space.                                    |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------+

Response Parameters
-------------------

None

Example Requests
----------------

Creating instance tags with tag keys key1 and key2 and tag values value1 and value2

.. code-block:: text

   POST https://{endpoint}/v2/{project_id}/kafka/{instance_id}/tags/action

   {
     "action" : "create",
     "tags" : [ {
       "key" : "key1",
       "value" : "value1"
     }, {
       "key" : "key2",
       "value" : "value2"
     } ]
   }

Example Responses
-----------------

None

Status Codes
------------

=========== =======================================
Status Code Description
=========== =======================================
204         Tags are successfully added or deleted.
=========== =======================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
