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

   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                                               |
   +=============+===========+========+===========================================================================================================+
   | project_id  | Yes       | String | Project ID. For details about how to obtain it, see :ref:`Obtaining a Project ID <kafka-api-0036212547>`. |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                                              |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+

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

   +-----------------------+-----------------------+-------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                             |
   +=======================+=======================+=========================================================================+
   | key                   | String                | Tag key.                                                                |
   |                       |                       |                                                                         |
   |                       |                       | -  Must be specified.                                                   |
   |                       |                       |                                                                         |
   |                       |                       | -  Must be unique for the same instance.                                |
   |                       |                       |                                                                         |
   |                       |                       | -  Can contain 1 to 128 characters.                                     |
   |                       |                       |                                                                         |
   |                       |                       | -  Can contain letters, digits, spaces, and special characters \_.:=+-@ |
   |                       |                       |                                                                         |
   |                       |                       | -  Cannot start or end with a space.                                    |
   +-----------------------+-----------------------+-------------------------------------------------------------------------+
   | value                 | String                | Tag value.                                                              |
   |                       |                       |                                                                         |
   |                       |                       | -  Can contain 0 to 255 characters.                                     |
   |                       |                       |                                                                         |
   |                       |                       | -  Can contain letters, digits, spaces, and special characters \_.:=+-@ |
   |                       |                       |                                                                         |
   |                       |                       | -  Cannot start or end with a space.                                    |
   +-----------------------+-----------------------+-------------------------------------------------------------------------+

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
