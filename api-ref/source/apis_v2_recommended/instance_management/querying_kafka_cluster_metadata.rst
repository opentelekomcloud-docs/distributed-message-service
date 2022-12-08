:original_name: ShowCluster.html

.. _ShowCluster:

Querying Kafka Cluster Metadata
===============================

Function
--------

This API is used to query Kafka cluster metadata.

URI
---

GET /v2/{project_id}/instances/{instance_id}/management/cluster

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

   +-----------+-------------------------------------------------------+----------------------------+
   | Parameter | Type                                                  | Description                |
   +===========+=======================================================+============================+
   | cluster   | :ref:`cluster <showcluster__response_cluster>` object | Cluster basic information. |
   +-----------+-------------------------------------------------------+----------------------------+

.. _showcluster__response_cluster:

.. table:: **Table 3** cluster

   +-------------------------+-----------------------------------------------------------------+------------------------------------------+
   | Parameter               | Type                                                            | Description                              |
   +=========================+=================================================================+==========================================+
   | controller              | String                                                          | Controller ID.                           |
   +-------------------------+-----------------------------------------------------------------+------------------------------------------+
   | brokers                 | Array of :ref:`brokers <showcluster__response_brokers>` objects | Broker list.                             |
   +-------------------------+-----------------------------------------------------------------+------------------------------------------+
   | topics_count            | Integer                                                         | Number of topics.                        |
   +-------------------------+-----------------------------------------------------------------+------------------------------------------+
   | partitions_count        | Integer                                                         | Number of partitions.                    |
   +-------------------------+-----------------------------------------------------------------+------------------------------------------+
   | online_partitions_count | Integer                                                         | Number of online partitions.             |
   +-------------------------+-----------------------------------------------------------------+------------------------------------------+
   | replicas_count          | Integer                                                         | Number of replicas.                      |
   +-------------------------+-----------------------------------------------------------------+------------------------------------------+
   | isr_replicas_count      | Integer                                                         | Total number of in-sync replicas (ISRs). |
   +-------------------------+-----------------------------------------------------------------+------------------------------------------+
   | consumers_count         | Integer                                                         | Number of consumer groups.               |
   +-------------------------+-----------------------------------------------------------------+------------------------------------------+

.. _showcluster__response_brokers:

.. table:: **Table 4** brokers

   +---------------+---------+------------------------------------------------------+
   | Parameter     | Type    | Description                                          |
   +===============+=========+======================================================+
   | host          | String  | Broker IP address.                                   |
   +---------------+---------+------------------------------------------------------+
   | port          | Integer | Port number.                                         |
   +---------------+---------+------------------------------------------------------+
   | broker_id     | String  | Broker ID.                                           |
   +---------------+---------+------------------------------------------------------+
   | is_controller | Boolean | Whether the broker is a controller.                  |
   +---------------+---------+------------------------------------------------------+
   | version       | String  | Server version.                                      |
   +---------------+---------+------------------------------------------------------+
   | register_time | Long    | Broker registration time, which is a Unix timestamp. |
   +---------------+---------+------------------------------------------------------+
   | is_health     | Boolean | Whether Kafka brokers can be connected.              |
   +---------------+---------+------------------------------------------------------+

Example Requests
----------------

.. code-block:: text

   GET https://{endpoint}/v2/{project_id}/instances/{instance_id}/management/cluster

Example Responses
-----------------

**Status code: 200**

Kafka cluster metadata is queried successfully.

.. code-block::

   {
     "cluster" : {
       "controller" : "2",
       "brokers" : [ {
         "host" : "192.168.0.159",
         "port" : 9093,
         "broker_id" : "0",
         "is_controller" : false,
         "version" : "1.1.0",
         "register_time" : 1588754647872,
         "is_health" : true
       }, {
         "host" : "192.168.0.48",
         "port" : 9093,
         "broker_id" : "1",
         "is_controller" : false,
         "version" : "1.1.0",
         "register_time" : 1588754647653,
         "is_health" : true
       }, {
         "host" : "192.168.0.212",
         "port" : 9093,
         "broker_id" : "2",
         "is_controller" : true,
         "version" : "1.1.0",
         "register_time" : 1588754647284,
         "is_health" : true
       } ],
       "topics_count" : 3,
       "partitions_count" : 9,
       "online_partitions_count" : 9,
       "replicas_count" : 27,
       "isr_replicas_count" : 27,
       "consumers_count" : 0
     }
   }

Status Codes
------------

=========== ===============================================
Status Code Description
=========== ===============================================
200         Kafka cluster metadata is queried successfully.
=========== ===============================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
