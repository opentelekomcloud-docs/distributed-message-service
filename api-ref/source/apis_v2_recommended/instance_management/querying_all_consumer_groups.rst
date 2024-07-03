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

   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                                               |
   +=============+===========+========+===========================================================================================================+
   | project_id  | Yes       | String | Project ID. For details about how to obtain it, see :ref:`Obtaining a Project ID <kafka-api-0036212547>`. |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                                              |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+

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

   +-----------+------------------------------------------------------------------------------------------------+----------------------------------+
   | Parameter | Type                                                                                           | Description                      |
   +===========+================================================================================================+==================================+
   | groups    | Array of :ref:`GroupInfoSimple <listinstanceconsumergroups__response_groupinfosimple>` objects | All consumer groups.             |
   +-----------+------------------------------------------------------------------------------------------------+----------------------------------+
   | total     | Integer                                                                                        | Total number of consumer groups. |
   +-----------+------------------------------------------------------------------------------------------------+----------------------------------+

.. _listinstanceconsumergroups__response_groupinfosimple:

.. table:: **Table 4** GroupInfoSimple

   +-----------------------+-----------------------+----------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                          |
   +=======================+=======================+======================================================================+
   | createdAt             | Long                  | Creation time.                                                       |
   +-----------------------+-----------------------+----------------------------------------------------------------------+
   | group_id              | String                | Consumer group ID.                                                   |
   +-----------------------+-----------------------+----------------------------------------------------------------------+
   | state                 | String                | Consumer group status. The value can be:                             |
   |                       |                       |                                                                      |
   |                       |                       | -  **Dead**: The consumer group has no members or metadata.          |
   |                       |                       |                                                                      |
   |                       |                       | -  **Empty**: The consumer group has metadata but has no members.    |
   |                       |                       |                                                                      |
   |                       |                       | -  **PreparingRebalance**: The consumer group is to be rebalanced.   |
   |                       |                       |                                                                      |
   |                       |                       | -  **CompletingRebalance**: All members have joined the group.       |
   |                       |                       |                                                                      |
   |                       |                       | -  **Stable**: Members in the consumer group can consume messages. " |
   +-----------------------+-----------------------+----------------------------------------------------------------------+
   | coordinator_id        | Integer               | Coordinator ID.                                                      |
   +-----------------------+-----------------------+----------------------------------------------------------------------+
   | group_desc            | String                | Consumer group description.                                          |
   +-----------------------+-----------------------+----------------------------------------------------------------------+
   | lag                   | Long                  | Number of accumulated messages.                                      |
   +-----------------------+-----------------------+----------------------------------------------------------------------+

Example Requests
----------------

Querying the consumer group list

.. code-block:: text

   GET https://{endpoint}/v2/{project_id}/instances/{instance_id}/groups?offest={offest}&limit={limit}&group={group}

Example Responses
-----------------

**Status code: 200**

All consumer groups are queried successfully.

.. code-block::

   {
     "groups" : [ {
       "createdAt" : 1691401194847,
       "group_id" : "consumer-1",
       "state" : "EMPTY",
       "coordinator_id" : 1,
       "lag" : 0,
       "group_desc" : null
     }, {
       "createdAt" : 1691401194960,
       "group_id" : "consumer-2",
       "state" : "STABLE",
       "coordinator_id" : 2,
       "lag" : 0,
       "group_desc" : null
     }, {
       "createdAt" : 1691401207309,
       "group_id" : "consumer-3",
       "state" : "STABLE",
       "coordinator_id" : 3,
       "lag" : 0,
       "group_desc" : null
     } ],
     "total" : 3
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
