:original_name: ShowKafkaProjectTags.html

.. _ShowKafkaProjectTags:

Listing Tags of a Project
=========================

Function
--------

This API is used to query project tags.

URI
---

GET /v2/{project_id}/kafka/tags

.. table:: **Table 1** Path Parameters

   ========== ========= ====== ===========
   Parameter  Mandatory Type   Description
   ========== ========= ====== ===========
   project_id Yes       String Project ID.
   ========== ========= ====== ===========

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameters

   +-----------+--------------------------------------------------------------------------------------------------+-------------+
   | Parameter | Type                                                                                             | Description |
   +===========+==================================================================================================+=============+
   | tags      | Array of :ref:`TagMultyValueEntity <showkafkaprojecttags__response_tagmultyvalueentity>` objects | Tag list.   |
   +-----------+--------------------------------------------------------------------------------------------------+-------------+

.. _showkafkaprojecttags__response_tagmultyvalueentity:

.. table:: **Table 3** TagMultyValueEntity

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                          |
   +=======================+=======================+======================================================================================================+
   | key                   | String                | Tag key, which can contain a maximum of 36 Unicode characters.                                       |
   |                       |                       |                                                                                                      |
   |                       |                       | The key cannot be left blank or be an empty string.                                                  |
   |                       |                       |                                                                                                      |
   |                       |                       | It cannot contain nonprintable ASCII (0-31) characters and the following special characters: =*<>,|/ |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------+
   | values                | Array of strings      | Tag value, which can contain a maximum of 43 Unicode characters.                                     |
   |                       |                       |                                                                                                      |
   |                       |                       | The value cannot be left blank or be an empty string.                                                |
   |                       |                       |                                                                                                      |
   |                       |                       | It cannot contain nonprintable ASCII (0-31) characters and the following special characters: =*<>,|/ |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------+

Example Requests
----------------

.. code-block:: text

   GET https://{endpoint}/v2/{project_id}/kafka/tags

Example Responses
-----------------

**Status code: 200**

The project tags are listed successfully.

.. code-block::

   {
     "tags" : [ {
       "key" : "key1",
       "values" : [ "value-test", "value1" ]
     }, {
       "key" : "key2",
       "values" : [ "value2" ]
     } ]
   }

Status Codes
------------

=========== =========================================
Status Code Description
=========== =========================================
200         The project tags are listed successfully.
=========== =========================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
