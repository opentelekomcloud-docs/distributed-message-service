:original_name: ListConnectorTasks.html

.. _ListConnectorTasks:

Querying Smart Connect Tasks
============================

Function
--------

This API is used to query Smart Connect tasks.

URI
---

GET /v2/{project_id}/instances/{instance_id}/connector/tasks

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                        |
   +=============+===========+========+====================================================================================+
   | project_id  | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <kafka-api-0036212547>`. |
   +-------------+-----------+--------+------------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                       |
   +-------------+-----------+--------+------------------------------------------------------------------------------------+

.. table:: **Table 2** Query Parameters

   +-----------+-----------+---------+------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Mandatory | Type    | Description                                                                                                            |
   +===========+===========+=========+========================================================================================================================+
   | offset    | No        | Integer | Offset, which is the position where the query starts. The value must be greater than or equal to 0.                    |
   +-----------+-----------+---------+------------------------------------------------------------------------------------------------------------------------+
   | limit     | No        | Integer | Maximum number of instances returned in the current query. The default value is **10**. The value ranges from 1 to 50. |
   +-----------+-----------+---------+------------------------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +--------------+------------------------------------------------------------------------------------------------------+----------------------------------------+
   | Parameter    | Type                                                                                                 | Description                            |
   +==============+======================================================================================================+========================================+
   | tasks        | Array of :ref:`SmartConnectTaskEntity <listconnectortasks__response_smartconnecttaskentity>` objects | Smart Connect task details.            |
   +--------------+------------------------------------------------------------------------------------------------------+----------------------------------------+
   | total_number | Integer                                                                                              | Number of Smart Connect tasks.         |
   +--------------+------------------------------------------------------------------------------------------------------+----------------------------------------+
   | max_tasks    | Integer                                                                                              | Maximum number of Smart Connect tasks. |
   +--------------+------------------------------------------------------------------------------------------------------+----------------------------------------+
   | quota_tasks  | Integer                                                                                              | Smart Connect task quota.              |
   +--------------+------------------------------------------------------------------------------------------------------+----------------------------------------+

.. _listconnectortasks__response_smartconnecttaskentity:

.. table:: **Table 4** SmartConnectTaskEntity

   +--------------+----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------+
   | Parameter    | Type                                                                                                           | Description                                              |
   +==============+================================================================================================================+==========================================================+
   | task_name    | String                                                                                                         | Smart Connect task name.                                 |
   +--------------+----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------+
   | topics       | String                                                                                                         | Topic of a Smart Connect task.                           |
   +--------------+----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------+
   | topics_regex | String                                                                                                         | Regular expression of the topic of a Smart Connect task. |
   +--------------+----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------+
   | source_type  | String                                                                                                         | Source type of a Smart Connect task.                     |
   +--------------+----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------+
   | source_task  | :ref:`SmartConnectTaskRespSourceConfig <listconnectortasks__response_smartconnecttaskrespsourceconfig>` object | Source configuration of a Smart Connect task.            |
   +--------------+----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------+
   | sink_type    | String                                                                                                         | Target type of a Smart Connect task.                     |
   +--------------+----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------+
   | sink_task    | :ref:`SmartConnectTaskRespSinkConfig <listconnectortasks__response_smartconnecttaskrespsinkconfig>` object     | Target type of a Smart Connect task.                     |
   +--------------+----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------+
   | id           | String                                                                                                         | ID of a Smart Connect task.                              |
   +--------------+----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------+
   | status       | String                                                                                                         | Smart Connect task status.                               |
   +--------------+----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------+
   | create_time  | Long                                                                                                           | Time when the Smart Connect task was created.            |
   +--------------+----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------+

.. _listconnectortasks__response_smartconnecttaskrespsourceconfig:

.. table:: **Table 5** SmartConnectTaskRespSourceConfig

   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                     | Type    | Description                                                                                                                                                                          |
   +===============================+=========+======================================================================================================================================================================================+
   | redis_address                 | String  | Redis instance address. (Displayed only when the source type is Redis.)                                                                                                              |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | redis_type                    | String  | Redis instance type. (Displayed only when the source type is Redis.)                                                                                                                 |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | dcs_instance_id               | String  | DCS instance ID. (Displayed only when the source type is Redis.)                                                                                                                     |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | sync_mode                     | String  | Synchronization type: **RDB_ONLY** indicates full synchronization; **CUSTOM_OFFSET** indicates full and incremental synchronization. (Displayed only when the source type is Redis.) |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | full_sync_wait_ms             | Integer | Interval of full synchronization retries, in ms. (Displayed only when the source type is Redis.)                                                                                     |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | full_sync_max_retry           | Integer | Max. retries of full synchronization. (Displayed only when the source type is Redis.)                                                                                                |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ratelimit                     | Integer | Rate limit, in KB/s. **-1**: disable. (Displayed only when the source type is Redis.)                                                                                                |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | current_cluster_name          | String  | Current Kafka instance name. (Displayed only when the source type is Kafka.)                                                                                                         |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | cluster_name                  | String  | Target Kafka instance name. (Displayed only when the source type is Kafka.)                                                                                                          |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | user_name                     | String  | Username of the target Kafka instance. (Displayed only when the source type is Kafka.)                                                                                               |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | sasl_mechanism                | String  | Target Kafka authentication mode. (Displayed only when the source type is Kafka.)                                                                                                    |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | instance_id                   | String  | Target Kafka instance ID. (Displayed only when the source type is Kafka.)                                                                                                            |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | bootstrap_servers             | String  | Target Kafka instance address. (Displayed only when the source type is Kafka.)                                                                                                       |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | security_protocol             | String  | Target Kafka authentication. (Displayed only when the source type is Kafka.)                                                                                                         |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | direction                     | String  | Sync direction. (Displayed only when the source type is Kafka.)                                                                                                                      |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | sync_consumer_offsets_enabled | Boolean | Indicates whether to sync the consumption progress. (Displayed only when the source type is Kafka.)                                                                                  |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | replication_factor            | Integer | Number of replicas. (Displayed only when the source type is Kafka.)                                                                                                                  |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | task_num                      | Integer | Number of tasks. (Displayed only when the source type is Kafka.)                                                                                                                     |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | rename_topic_enabled          | Boolean | Indicates whether to rename a topic. (Displayed only when the source type is Kafka.)                                                                                                 |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | provenance_header_enabled     | Boolean | Indicates whether to add the source header. (Displayed only when the source type is Kafka.)                                                                                          |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | consumer_strategy             | String  | Start offset. **latest**: Obtain the latest data; **earliest**: Obtain the earliest data. (Displayed only when the source type is Kafka.)                                            |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | compression_type              | String  | Compression algorithm. (Displayed only when the source type is Kafka.)                                                                                                               |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | topics_mapping                | String  | Topic mapping. (Displayed only when the source type is Kafka.)                                                                                                                       |
   +-------------------------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _listconnectortasks__response_smartconnecttaskrespsinkconfig:

.. table:: **Table 6** SmartConnectTaskRespSinkConfig

   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter              | Type    | Description                                                                                                                                                     |
   +========================+=========+=================================================================================================================================================================+
   | redis_address          | String  | Redis instance address. (Displayed only when the target type is Redis.)                                                                                         |
   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | redis_type             | String  | Redis instance type. (Displayed only when the target type is Redis.)                                                                                            |
   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | dcs_instance_id        | String  | DCS instance ID. (Displayed only when the target type is Redis.)                                                                                                |
   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | target_db              | Integer | Target database. The default value is **-1**. (Displayed only when the target type is Redis.)                                                                   |
   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | consumer_strategy      | String  | Start offset. **latest**: Obtain the latest data; **earliest**: Obtain the earliest data. (Displayed only when the target type is OBS.)                         |
   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | destination_file_type  | String  | Dump file format. Only **TEXT** is supported. (Displayed only when the target type is OBS.)                                                                     |
   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | deliver_time_interval  | Integer | Dumping period (s). (Displayed only when the target type is OBS.)                                                                                               |
   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | obs_bucket_name        | String  | Dumping address. (Displayed only when the target type is OBS.)                                                                                                  |
   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | obs_path               | String  | Dump directory. (Displayed only when the target type is OBS.)                                                                                                   |
   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | partition_format       | String  | Time directory format. (Displayed only when the target type is OBS.)                                                                                            |
   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | record_delimiter       | String  | Line break. (Displayed only when the target type is OBS.)                                                                                                       |
   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | store_keys             | Boolean | Storage key. (Displayed only when the target type is OBS.)                                                                                                      |
   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | obs_part_size          | Integer | Size (in bytes) of each file to be uploaded. The default value is **5242880**. (Displayed only when the target type is OBS.)                                    |
   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | flush_size             | Integer | flush_size. (Displayed only when the target type is OBS.)                                                                                                       |
   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | timezone               | String  | Time zone. (Displayed only when the target type is OBS.)                                                                                                        |
   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | schema_generator_class | String  | schema_generator class. The default value is **io.confluent.connect.storage.hive.schema.DefaultSchemaGenerator**. (Displayed only when the target type is OBS.) |
   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | partitioner_class      | String  | partitioner class. The default value is **io.confluent.connect.storage.partitioner.TimeBasedPartitioner**. (Displayed only when the target type is OBS.)        |
   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | value_converter        | String  | value_converter. The default value is **org.apache.kafka.connect.converters.ByteArrayConverter**. (Displayed only when the target type is OBS.)                 |
   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | key_converter          | String  | key_converter. The default value is **org.apache.kafka.connect.converters.ByteArrayConverter**. (Displayed only when the target type is OBS.)                   |
   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | kv_delimiter           | String  | kv_delimiter. The default value is **:**. (Displayed only when the target type is OBS.)                                                                         |
   +------------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+

Example Requests
----------------

None

Example Responses
-----------------

**Status code: 200**

Successful.

.. code-block::

   {
     "tasks" : [ {
       "task_name" : "smart-connect-1571576841",
       "topics" : "topic-1643449744",
       "source_task" : {
         "current_cluster_name" : "A",
         "cluster_name" : "B",
         "direction" : "pull",
         "bootstrap_servers" : "192.168.45.58:9092,192.168.44.1:9092,192.168.41.230:9092,192.168.43.112:9092",
         "instance_id" : "59f6d088-****-****-****-********",
         "consumer_strategy" : "earliest",
         "sync_consumer_offsets_enabled" : false,
         "rename_topic_enabled" : false,
         "provenance_header_enabled" : false,
         "security_protocol" : "PLAINTEXT",
         "sasl_mechanism" : "PLAIN",
         "user_name" : "",
         "topics_mapping" : "",
         "compression_type" : "none",
         "task_num" : 2,
         "replication_factor" : 3
       },
       "source_type" : "KAFKA_REPLICATOR_SOURCE",
       "sink_task" : null,
       "sink_type" : "NONE",
       "id" : "194917d0-****-****-****-********",
       "status" : "RUNNING",
       "create_time" : 1708427753133
     }, {
       "task_name" : "smart-connect-1",
       "topics_regex" : "topic-obs*",
       "source_task" : null,
       "source_type" : "NONE",
       "sink_task" : {
         "consumer_strategy" : "earliest",
         "destination_file_type" : "TEXT",
         "obs_bucket_name" : "abcabc",
         "obs_path" : "obsTransfer-1810125534",
         "partition_format" : "yyyy/MM/dd/HH/mm",
         "record_delimiter" : "\\n",
         "deliver_time_interva" : 300,
         "obs_part_size" : 5242880,
         "flush_size" : 1000000,
         "timezone" : "Asia/Chongqing",
         "schema_generator_class" : "io.confluent.connect.storage.hive.schema.DefaultSchemaGenerator",
         "partitioner_class" : "io.confluent.connect.storage.partitioner.TimeBasedPartitioner",
         "value_converter" : "org.apache.kafka.connect.converters.ByteArrayConverter",
         "key_converter" : "org.apache.kafka.connect.converters.ByteArrayConverter",
         "store_keys" : false,
         "kv_delimiter" : ":"
       },
       "sink_type" : "OBS_SINK",
       "id" : "3c0ac4d1-****-****-****-********",
       "status" : "RUNNING",
       "create_time" : 1708565483911
     }, {
       "task_name" : "smart-connect-121248117",
       "topics" : "topic-sc",
       "source_task" : {
         "redis_address" : "192.168.91.179:6379",
         "redis_type" : "standalone",
         "dcs_instance_id" : "949190a2-598a-4afd-99a8-dad3cae1e7cd",
         "sync_mode" : "RDB_ONLY",
         "full_sync_wait_ms" : 13000,
         "full_sync_max_retry" : 4,
         "ratelimit" : -1
       },
       "source_type" : "REDIS_REPLICATOR_SOURCE",
       "sink_task" : {
         "redis_address" : "192.168.119.51:6379",
         "redis_type" : "standalone",
         "dcs_instance_id" : "9b981368-a8e3-416a-87d9-1581a968b41b",
         "target_db" : -1
       },
       "sink_type" : "REDIS_REPLICATOR_SINK",
       "id" : "8a205bbd-****-****-****-********",
       "status" : "RUNNING",
       "create_time" : 1708427753133
     } ],
     "total_number" : 3,
     "max_tasks" : 18,
     "quota_tasks" : 18
   }

Status Codes
------------

=========== ===========
Status Code Description
=========== ===========
200         Successful.
=========== ===========

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
