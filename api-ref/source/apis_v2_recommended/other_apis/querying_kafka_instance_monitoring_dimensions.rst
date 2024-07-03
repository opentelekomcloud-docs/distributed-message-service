:original_name: ShowCesHierarchy.html

.. _ShowCesHierarchy:

Querying Kafka Instance Monitoring Dimensions
=============================================

Function
--------

This API is used to query Kafka instance monitoring dimensions.

URI
---

GET /v2/{project_id}/instances/{instance_id}/ces-hierarchy

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

   +--------------+--------------------------------------------------------------------------------+-----------------------------+
   | Parameter    | Type                                                                           | Description                 |
   +==============+================================================================================+=============================+
   | dimensions   | Array of :ref:`dimensions <showceshierarchy__response_dimensions>` objects     | Monitoring dimensions.      |
   +--------------+--------------------------------------------------------------------------------+-----------------------------+
   | instance_ids | Array of :ref:`instance_ids <showceshierarchy__response_instance_ids>` objects | Instance information.       |
   +--------------+--------------------------------------------------------------------------------+-----------------------------+
   | nodes        | Array of :ref:`nodes <showceshierarchy__response_nodes>` objects               | Broker information.         |
   +--------------+--------------------------------------------------------------------------------+-----------------------------+
   | queues       | Array of :ref:`queues <showceshierarchy__response_queues>` objects             | Topic information.          |
   +--------------+--------------------------------------------------------------------------------+-----------------------------+
   | groups       | Array of :ref:`groups <showceshierarchy__response_groups>` objects             | Consumer group information. |
   +--------------+--------------------------------------------------------------------------------+-----------------------------+

.. _showceshierarchy__response_dimensions:

.. table:: **Table 3** dimensions

   +------------+------------------------------------------------------------------------+--------------------------------+
   | Parameter  | Type                                                                   | Description                    |
   +============+========================================================================+================================+
   | name       | String                                                                 | Monitoring dimension name.     |
   +------------+------------------------------------------------------------------------+--------------------------------+
   | metrics    | Array of strings                                                       | Metric name.                   |
   +------------+------------------------------------------------------------------------+--------------------------------+
   | key_name   | Array of strings                                                       | Key used for monitoring query. |
   +------------+------------------------------------------------------------------------+--------------------------------+
   | dim_router | Array of strings                                                       | Monitoring dimension route.    |
   +------------+------------------------------------------------------------------------+--------------------------------+
   | children   | Array of :ref:`children <showceshierarchy__response_children>` objects | List of secondary dimensions.  |
   +------------+------------------------------------------------------------------------+--------------------------------+

.. _showceshierarchy__response_children:

.. table:: **Table 4** children

   ========== ================ ===================================
   Parameter  Type             Description
   ========== ================ ===================================
   name       String           Secondary dimension name.
   metrics    Array of strings Metrics on the secondary dimension.
   key_name   Array of strings Key used for monitoring query.
   dim_router Array of strings Monitoring dimension route.
   ========== ================ ===================================

.. _showceshierarchy__response_instance_ids:

.. table:: **Table 5** instance_ids

   ========= ====== ============
   Parameter Type   Description
   ========= ====== ============
   name      String Instance ID.
   ========= ====== ============

.. _showceshierarchy__response_nodes:

.. table:: **Table 6** nodes

   ========= ====== ============
   Parameter Type   Description
   ========= ====== ============
   name      String Broker name.
   ========= ====== ============

.. _showceshierarchy__response_queues:

.. table:: **Table 7** queues

   +------------+----------------------------------------------------------------------------+-----------------+
   | Parameter  | Type                                                                       | Description     |
   +============+============================================================================+=================+
   | name       | String                                                                     | Topic name.     |
   +------------+----------------------------------------------------------------------------+-----------------+
   | partitions | Array of :ref:`partitions <showceshierarchy__response_partitions>` objects | Partition list. |
   +------------+----------------------------------------------------------------------------+-----------------+

.. _showceshierarchy__response_partitions:

.. table:: **Table 8** partitions

   ========= ====== ===============
   Parameter Type   Description
   ========= ====== ===============
   name      String Partition name.
   ========= ====== ===============

.. _showceshierarchy__response_groups:

.. table:: **Table 9** groups

   +-----------+----------------------------------------------------------------------+----------------------+
   | Parameter | Type                                                                 | Description          |
   +===========+======================================================================+======================+
   | name      | String                                                               | Consumer group name. |
   +-----------+----------------------------------------------------------------------+----------------------+
   | queues    | Array of :ref:`queues <showceshierarchy__response_queues_1>` objects | Topic information.   |
   +-----------+----------------------------------------------------------------------+----------------------+

.. _showceshierarchy__response_queues_1:

.. table:: **Table 10** queues

   +------------+------------------------------------------------------------------------------+------------------------+
   | Parameter  | Type                                                                         | Description            |
   +============+==============================================================================+========================+
   | name       | String                                                                       | Topic name.            |
   +------------+------------------------------------------------------------------------------+------------------------+
   | partitions | Array of :ref:`partitions <showceshierarchy__response_partitions_1>` objects | Partition information. |
   +------------+------------------------------------------------------------------------------+------------------------+

.. _showceshierarchy__response_partitions_1:

.. table:: **Table 11** partitions

   ========= ====== ===============
   Parameter Type   Description
   ========= ====== ===============
   name      String Partition name.
   ========= ====== ===============

Example Requests
----------------

.. code-block:: text

   GET https://{endpoint}/v2/{project_id}/instances/{instance_id}/ces-hierarchy

Example Responses
-----------------

**Status code: 200**

Query succeeded.

.. code-block::

   {
     "dimensions" : [ {
       "name" : "kafka_instance_id",
       "metrics" : [ "current_partitions", "current_topics", "group_messages" ],
       "key_name" : [ "instance_ids" ],
       "dim_router" : [ "kafka_instance_id" ]
     }, {
       "name" : "kafka_broker",
       "metrics" : [ "broker_data_size", "broker_messages_in_rate", "broker_bytes_out_rate", "broker_bytes_in_rate", "broker_produce_mean", "broker_fetch_mean" ],
       "key_name" : [ "nodes" ],
       "dim_router" : [ "kafka_instance_id", "kafka_broker" ]
     }, {
       "name" : "kafka_rest",
       "metrics" : [ "rest_produce_success", "rest_produce_failed", "rest_produce_latency", "rest_produce_msg_num", "rest_produce_flow", "rest_consume_success", "rest_consume_failed", "rest_consume_latency", "rest_consume_msg_num", "rest_consume_flow", "rest_commit_success", "rest_commit_failed", "rest_commit_latency", "rest_commit_msg_num", "rest_commit_flow" ],
       "key_name" : [ "nodes" ],
       "dim_router" : [ "kafka_instance_id", "kafka_rest" ]
     }, {
       "name" : "kafka_topics",
       "metrics" : [ "topic_data_size", "topic_messages_in_rate", "topic_bytes_out_rate", "topic_bytes_in_rate", "topic_messages" ],
       "key_name" : [ "queues" ],
       "dim_router" : [ "kafka_instance_id", "kafka_topics" ],
       "children" : [ {
         "name" : "kafka_partitions",
         "metrics" : [ "produced_messages", "partition_messages" ],
         "key_name" : [ "queues", "partitions" ],
         "dim_router" : [ "kafka_instance_id", "kafka_topics", "kafka_partitions" ]
       } ]
     }, {
       "name" : "kafka_groups_partitions",
       "metrics" : [ "messages_consumed", "messages_remained" ],
       "key_name" : [ "groups", "queues", "partitions" ],
       "dim_router" : [ "kafka_instance_id", "kafka_groups", "kafka_groups_topics", "kafka_groups_partitions" ]
     } ],
     "instance_ids" : [ {
       "name" : "68f3f6a0-3741-453b-bda9-a6ff6b5bb6f7"
     } ],
     "nodes" : [ {
       "name" : "broker-0"
     }, {
       "name" : "broker-1"
     }, {
       "name" : "broker-2"
     } ],
     "queues" : [ {
       "name" : "aaaa",
       "partitions" : [ {
         "name" : "0"
       } ]
     }, {
       "name" : "mytest",
       "partitions" : [ {
         "name" : "0"
       }, {
         "name" : "1"
       }, {
         "name" : "2"
       } ]
     }, {
       "name" : "topic-84234378",
       "partitions" : [ {
         "name" : "0"
       }, {
         "name" : "1"
       }, {
         "name" : "2"
       } ]
     } ],
     "groups" : [ {
       "name" : "test-consumer-group",
       "queues" : [ {
         "name" : "mytest",
         "partitions" : [ {
           "name" : "0"
         }, {
           "name" : "1"
         }, {
           "name" : "2"
         } ]
       } ]
     } ]
   }

Status Codes
------------

=========== ================
Status Code Description
=========== ================
200         Query succeeded.
=========== ================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
