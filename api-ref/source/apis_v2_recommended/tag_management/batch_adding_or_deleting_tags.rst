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

   =========== ========= ====== ============
   Parameter   Mandatory Type   Description
   =========== ========= ====== ============
   project_id  Yes       String Project ID.
   instance_id Yes       String Instance ID.
   =========== ========= ====== ============

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

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                          |
   +=================+=================+=================+======================================================================================================+
   | key             | No              | String          | Tag key, which can contain a maximum of 36 Unicode characters.                                       |
   |                 |                 |                 |                                                                                                      |
   |                 |                 |                 | The key cannot be left blank or be an empty string.                                                  |
   |                 |                 |                 |                                                                                                      |
   |                 |                 |                 | It cannot contain nonprintable ASCII (0-31) characters and the following special characters: =*<>,|/ |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------+
   | value           | No              | String          | Tag value, which can contain a maximum of 43 Unicode characters.                                     |
   |                 |                 |                 |                                                                                                      |
   |                 |                 |                 | The value cannot be left blank or be an empty string.                                                |
   |                 |                 |                 |                                                                                                      |
   |                 |                 |                 | It cannot contain nonprintable ASCII (0-31) characters and the following special characters: =*<>,|/ |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

None

Example Requests
----------------

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
