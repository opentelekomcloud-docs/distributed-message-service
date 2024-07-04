:original_name: ShowKafkaTopicPartitionDiskusage.html

.. _ShowKafkaTopicPartitionDiskusage:

Querying the Disk Usage Status of Topics
========================================

Function
--------

This API is used to query the broker disk usage of topics.

URI
---

GET /v2/{project_id}/instances/{instance_id}/topics/diskusage

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                                               |
   +=============+===========+========+===========================================================================================================+
   | project_id  | Yes       | String | Project ID. For details about how to obtain it, see :ref:`Obtaining a Project ID <kafka-api-0036212547>`. |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                                              |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+

.. table:: **Table 2** Query Parameters

   +------------+-----------+--------+------------------------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type   | Description                                                                                    |
   +============+===========+========+================================================================================================+
   | minSize    | No        | String | Querying partitions by the used disk space. Options: 1 KB, 1 MB and 1 GB. Default value: 1 GB. |
   +------------+-----------+--------+------------------------------------------------------------------------------------------------+
   | top        | No        | String | Querying partitions by top disk usage.                                                         |
   +------------+-----------+--------+------------------------------------------------------------------------------------------------+
   | percentage | No        | String | Querying partitions by the percentage of the used disk space.                                  |
   +------------+-----------+--------+------------------------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-------------+------------------------------------------------------------------------------------------------------+--------------+
   | Parameter   | Type                                                                                                 | Description  |
   +=============+======================================================================================================+==============+
   | broker_list | Array of :ref:`DiskusageEntity <showkafkatopicpartitiondiskusage__response_diskusageentity>` objects | Broker list. |
   +-------------+------------------------------------------------------------------------------------------------------+--------------+

.. _showkafkatopicpartitiondiskusage__response_diskusageentity:

.. table:: **Table 4** DiskusageEntity

   +--------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------+
   | Parameter                | Type                                                                                                           | Description                    |
   +==========================+================================================================================================================+================================+
   | broker_name              | String                                                                                                         | Broker name.                   |
   +--------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------+
   | data_disk_size           | String                                                                                                         | Disk capacity.                 |
   +--------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------+
   | data_disk_use            | String                                                                                                         | Used disk space.               |
   +--------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------+
   | data_disk_free           | String                                                                                                         | Remaining disk space.          |
   +--------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------+
   | data_disk_use_percentage | String                                                                                                         | Message label.                 |
   +--------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------+
   | status                   | String                                                                                                         | Message label.                 |
   +--------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------+
   | topic_list               | Array of :ref:`DiskusageTopicEntity <showkafkatopicpartitiondiskusage__response_diskusagetopicentity>` objects | Disk usage list of the topics. |
   +--------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------+

.. _showkafkatopicpartitiondiskusage__response_diskusagetopicentity:

.. table:: **Table 5** DiskusageTopicEntity

   =============== ====== ==============================
   Parameter       Type   Description
   =============== ====== ==============================
   size            String Disk usage.
   topic_name      String Topic name.
   topic_partition String Partition.
   percentage      Double Percentage of used disk space.
   =============== ====== ==============================

Example Requests
----------------

Querying the disk usage status of topics

.. code-block:: text

   GET https://{endpoint}/v2/{project_id}/instances/{instance_id}/topics/diskusage

Example Responses
-----------------

**Status code: 200**

The query is successful.

.. code-block::

   {
     "broker_list" : [ {
       "broker_name" : "broker-0",
       "data_disk_size" : "66G",
       "data_disk_use" : "53M",
       "data_disk_free" : "63G",
       "data_disk_use_percentage" : "1",
       "status" : "Success get info",
       "topic_list" : [ {
         "size" : "12K",
         "topic_name" : "topic-test",
         "topic_partition" : "2",
         "percentage" : 1.7339533025568183E-5
       }, {
         "size" : "12K",
         "topic_name" : "__consumer_offsets",
         "topic_partition" : "4",
         "percentage" : 1.7339533025568183E-5
       }, {
         "size" : "12K",
         "topic_name" : "__consumer_offsets",
         "topic_partition" : "3",
         "percentage" : 1.7339533025568183E-5
       }, {
         "size" : "8.0K",
         "topic_name" : "__trace",
         "topic_partition" : "6",
         "percentage" : 1.1559688683712121E-5
       }, {
         "size" : "8.0K",
         "topic_name" : "__trace",
         "topic_partition" : "4",
         "percentage" : 1.1559688683712121E-5
       }, {
         "size" : "8.0K",
         "topic_name" : "__trace",
         "topic_partition" : "2",
         "percentage" : 1.1559688683712121E-5
       }, {
         "size" : "8.0K",
         "topic_name" : "__trace",
         "topic_partition" : "0",
         "percentage" : 1.1559688683712121E-5
       }, {
         "size" : "8.0K",
         "topic_name" : "topic-test",
         "topic_partition" : "0",
         "percentage" : 1.1559688683712121E-5
       }, {
         "size" : "8.0K",
         "topic_name" : "topic-1568537362",
         "topic_partition" : "2",
         "percentage" : 1.1559688683712121E-5
       }, {
         "size" : "8.0K",
         "topic_name" : "__consumer_offsets",
         "topic_partition" : "7",
         "percentage" : 1.1559688683712121E-5
       } ]
     } ]
   }

Status Codes
------------

=========== ========================
Status Code Description
=========== ========================
200         The query is successful.
=========== ========================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
