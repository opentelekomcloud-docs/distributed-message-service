:original_name: ShowKafkaTags.html

.. _ShowKafkaTags:

Listing Tags of an Instance
===========================

Function
--------

This API is used to query instance tags.

URI
---

GET /v2/{project_id}/kafka/{instance_id}/tags

.. table:: **Table 1** Path Parameters

   =========== ========= ====== ============
   Parameter   Mandatory Type   Description
   =========== ========= ====== ============
   project_id  Yes       String Project ID.
   instance_id Yes       String Instance ID.
   =========== ========= ====== ============

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameters

   +-----------+-----------------------------------------------------------------------+-------------+
   | Parameter | Type                                                                  | Description |
   +===========+=======================================================================+=============+
   | tags      | Array of :ref:`TagEntity <showkafkatags__response_tagentity>` objects | Tag list.   |
   +-----------+-----------------------------------------------------------------------+-------------+

.. _showkafkatags__response_tagentity:

.. table:: **Table 3** TagEntity

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                          |
   +=======================+=======================+======================================================================================================+
   | key                   | String                | Tag key, which can contain a maximum of 36 Unicode characters.                                       |
   |                       |                       |                                                                                                      |
   |                       |                       | The key cannot be left blank or be an empty string.                                                  |
   |                       |                       |                                                                                                      |
   |                       |                       | It cannot contain nonprintable ASCII (0-31) characters and the following special characters: =*<>,|/ |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------+
   | value                 | String                | Tag value, which can contain a maximum of 43 Unicode characters.                                     |
   |                       |                       |                                                                                                      |
   |                       |                       | The value cannot be left blank or be an empty string.                                                |
   |                       |                       |                                                                                                      |
   |                       |                       | It cannot contain nonprintable ASCII (0-31) characters and the following special characters: =*<>,|/ |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------+

Example Requests
----------------

.. code-block:: text

   GET https://{endpoint}/v2/{project_id}/kafka/{instance_id}/tags

Example Responses
-----------------

**Status code: 200**

The instance tags are listed successfully.

.. code-block::

   {
     "tags" : [ {
       "key" : "key1",
       "value" : "value1"
     }, {
       "key" : "key2",
       "value" : "value2"
     } ]
   }

Status Codes
------------

=========== ==========================================
Status Code Description
=========== ==========================================
200         The instance tags are listed successfully.
=========== ==========================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
