:original_name: ShowGroups.html

.. _ShowGroups:

Querying Consumer Group Details
===============================

Function
--------

This API is used to query consumer group details.

URI
---

GET /v2/{project_id}/instances/{instance_id}/management/groups/{group}

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                                               |
   +=============+===========+========+===========================================================================================================+
   | project_id  | Yes       | String | Project ID. For details about how to obtain it, see :ref:`Obtaining a Project ID <kafka-api-0036212547>`. |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                                              |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | group       | Yes       | String | Consumer group name.                                                                                      |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameters

   +-----------+--------------------------------------------------+-----------------------------+
   | Parameter | Type                                             | Description                 |
   +===========+==================================================+=============================+
   | group     | :ref:`group <showgroups__response_group>` object | Consumer group information. |
   +-----------+--------------------------------------------------+-----------------------------+

.. _showgroups__response_group:

.. table:: **Table 3** group

   +-----------------------+--------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------+
   | Parameter             | Type                                                                                       | Description                                                                 |
   +=======================+============================================================================================+=============================================================================+
   | group_id              | String                                                                                     | Consumer group name.                                                        |
   +-----------------------+--------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------+
   | state                 | String                                                                                     | Consumer group status. The value can be:                                    |
   |                       |                                                                                            |                                                                             |
   |                       |                                                                                            | -  **Dead**: The consumer group has no members and no metadata.             |
   |                       |                                                                                            |                                                                             |
   |                       |                                                                                            | -  **Empty**: The consumer group has metadata but has no members.           |
   |                       |                                                                                            |                                                                             |
   |                       |                                                                                            | -  **PreparingRebalance**: The consumer group is to be rebalanced.          |
   |                       |                                                                                            |                                                                             |
   |                       |                                                                                            | -  **CompletingRebalance**: All members have jointed the group.             |
   |                       |                                                                                            |                                                                             |
   |                       |                                                                                            | -  **Stable**: Members in the consumer group can consume messages normally. |
   +-----------------------+--------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------+
   | coordinator_id        | Integer                                                                                    | Coordinator ID.                                                             |
   +-----------------------+--------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------+
   | members               | Array of :ref:`members <showgroups__response_members>` objects                             | Consumer list.                                                              |
   +-----------------------+--------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------+
   | group_message_offsets | Array of :ref:`group_message_offsets <showgroups__response_group_message_offsets>` objects | Consumer offset.                                                            |
   +-----------------------+--------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------+
   | assignment_strategy   | String                                                                                     | Partition assignment policy.                                                |
   +-----------------------+--------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------+

.. _showgroups__response_members:

.. table:: **Table 4** members

   +------------+----------------------------------------------------------------------+-------------------------------------------------------+
   | Parameter  | Type                                                                 | Description                                           |
   +============+======================================================================+=======================================================+
   | host       | String                                                               | Consumer address.                                     |
   +------------+----------------------------------------------------------------------+-------------------------------------------------------+
   | assignment | Array of :ref:`assignment <showgroups__response_assignment>` objects | Details about the partition assigned to the consumer. |
   +------------+----------------------------------------------------------------------+-------------------------------------------------------+
   | member_id  | String                                                               | Consumer ID.                                          |
   +------------+----------------------------------------------------------------------+-------------------------------------------------------+
   | client_id  | String                                                               | Client ID.                                            |
   +------------+----------------------------------------------------------------------+-------------------------------------------------------+

.. _showgroups__response_assignment:

.. table:: **Table 5** assignment

   ========== ================= ===============
   Parameter  Type              Description
   ========== ================= ===============
   topic      String            Topic name.
   partitions Array of integers Partition list.
   ========== ================= ===============

.. _showgroups__response_group_message_offsets:

.. table:: **Table 6** group_message_offsets

   +------------------------+---------+--------------------------------------------------------------------------------------------------+
   | Parameter              | Type    | Description                                                                                      |
   +========================+=========+==================================================================================================+
   | partition              | Integer | Partition number.                                                                                |
   +------------------------+---------+--------------------------------------------------------------------------------------------------+
   | lag                    | Long    | Number of remaining messages that can be retrieved, that is, the number of accumulated messages. |
   +------------------------+---------+--------------------------------------------------------------------------------------------------+
   | topic                  | String  | Topic name.                                                                                      |
   +------------------------+---------+--------------------------------------------------------------------------------------------------+
   | message_current_offset | Long    | Consumer offset.                                                                                 |
   +------------------------+---------+--------------------------------------------------------------------------------------------------+
   | message_log_end_offset | Long    | Log end offset (LEO).                                                                            |
   +------------------------+---------+--------------------------------------------------------------------------------------------------+

Example Requests
----------------

.. code-block:: text

   GET https://{endpoint}/v2/{project_id}/instances/{instance_id}/management/groups/{group}

Example Responses
-----------------

**Status code: 200**

The consumer group details are queried successfully.

.. code-block::

   {
     "group" : {
       "members" : [ {
         "host" : "/172.31.1.102",
         "assignment" : [ {
           "topic" : "test",
           "partitions" : [ 0, 1, 2 ]
         } ],
         "member_id" : "consumer-1-6b8ee551-d499-47d4-9beb-ba1527496785",
         "client_id" : "consumer-1"
       } ],
       "state" : "STABLE",
       "group_id" : "test-consumer-group",
       "coordinator_id" : 2,
       "group_message_offsets" : [ {
         "partition" : 0,
         "lag" : 31396,
         "topic" : "test",
         "message_current_offset" : 935,
         "message_log_end_offset" : 32331
       }, {
         "partition" : 0,
         "lag" : 0,
         "topic" : "aaaa",
         "message_current_offset" : 0,
         "message_log_end_offset" : 0
       }, {
         "partition" : 1,
         "lag" : 31279,
         "topic" : "test",
         "message_current_offset" : 1058,
         "message_log_end_offset" : 32337
       }, {
         "partition" : 1,
         "lag" : 0,
         "topic" : "aaaa",
         "message_current_offset" : 0,
         "message_log_end_offset" : 0
       }, {
         "partition" : 2,
         "lag" : 31603,
         "topic" : "test",
         "message_current_offset" : 739,
         "message_log_end_offset" : 32342
       } ],
       "assignment_strategy" : "range"
     }
   }

Status Codes
------------

=========== ====================================================
Status Code Description
=========== ====================================================
200         The consumer group details are queried successfully.
=========== ====================================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
