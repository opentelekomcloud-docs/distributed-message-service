:original_name: ListInstanceConsumerGroups.html

.. _ListInstanceConsumerGroups:

Querying All Consumer Groups
============================

Function
--------

This API is used to query all consumer groups.

URI
---

GET /v2/{project_id}/instances/{instance_id}/groups

.. table:: **Table 1** Path Parameters

   =========== ========= ====== ============
   Parameter   Mandatory Type   Description
   =========== ========= ====== ============
   project_id  Yes       String Project ID.
   instance_id Yes       String Instance ID.
   =========== ========= ====== ============

.. table:: **Table 2** Query Parameters

   +-----------+-----------+--------+---------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Mandatory | Type   | Description                                                                                                                     |
   +===========+===========+========+=================================================================================================================================+
   | offset    | No        | String | Offset, which is the position where the query starts. The value must be greater than or equal to 0.                             |
   +-----------+-----------+--------+---------------------------------------------------------------------------------------------------------------------------------+
   | limit     | No        | String | Maximum number of consumer group IDs returned in the current query. The default value is **10**. The value ranges from 1 to 50. |
   +-----------+-----------+--------+---------------------------------------------------------------------------------------------------------------------------------+
   | group     | No        | String | Filter consumer group names that contain specific keywords.                                                                     |
   +-----------+-----------+--------+---------------------------------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-----------------+------------------+-------------------------------------------------+
   | Parameter       | Type             | Description                                     |
   +=================+==================+=================================================+
   | group_ids       | Array of strings | All consumer group IDs.                         |
   +-----------------+------------------+-------------------------------------------------+
   | total           | Integer          | Total number of consumer groups.                |
   +-----------------+------------------+-------------------------------------------------+
   | next_offset     | Integer          | Sequence number of the next consumer group.     |
   +-----------------+------------------+-------------------------------------------------+
   | previous_offset | Integer          | Sequence number of the previous consumer group. |
   +-----------------+------------------+-------------------------------------------------+

Example Requests
----------------

.. code-block:: text

   GET https://{endpoint}/v2/{project_id}/instances/{instance_id}/groups?offest={offest}&limit={limit}&group={group}

Example Responses
-----------------

**Status code: 200**

All consumer groups are queried successfully.

.. code-block::

   {
     "group_ids" : [ "groupId_1", "groupId_2", "groupId_3" ],
     "total" : 5,
     "next_offset" : 4,
     "previous_offset" : 0
   }

Status Codes
------------

=========== =============================================
Status Code Description
=========== =============================================
200         All consumer groups are queried successfully.
=========== =============================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
