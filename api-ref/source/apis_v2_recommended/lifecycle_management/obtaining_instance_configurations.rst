:original_name: ShowInstanceConfigs.html

.. _ShowInstanceConfigs:

Obtaining Instance Configurations
=================================

Function
--------

This API is used to obtain instance configurations.

URI
---

GET /v2/{project_id}/instances/{instance_id}/configs

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

   +---------------+---------------------------------------------------------------------------------------+-----------------------+
   | Parameter     | Type                                                                                  | Description           |
   +===============+=======================================================================================+=======================+
   | kafka_configs | Array of :ref:`InstanceConfig <showinstanceconfigs__response_instanceconfig>` objects | Kafka configurations. |
   +---------------+---------------------------------------------------------------------------------------+-----------------------+

.. _showinstanceconfigs__response_instanceconfig:

.. table:: **Table 3** InstanceConfig

   +---------------+--------+-----------------------------------------------------------------+
   | Parameter     | Type   | Description                                                     |
   +===============+========+=================================================================+
   | name          | String | Configuration name.                                             |
   +---------------+--------+-----------------------------------------------------------------+
   | valid_values  | String | Valid value.                                                    |
   +---------------+--------+-----------------------------------------------------------------+
   | default_value | String | Default value.                                                  |
   +---------------+--------+-----------------------------------------------------------------+
   | config_type   | String | Configuration type. The value can be **static** or **dynamic**. |
   +---------------+--------+-----------------------------------------------------------------+
   | value         | String | Current value.                                                  |
   +---------------+--------+-----------------------------------------------------------------+
   | value_type    | String | Value type.                                                     |
   +---------------+--------+-----------------------------------------------------------------+

Example Requests
----------------

.. code-block:: text

   GET https://{endpoint}/v2/{project_id}/instances/{instance_id}/configs

Example Responses
-----------------

**Status code: 200**

Configuration obtained.

.. code-block::

   {
     "kafka_configs" : [ {
       "name" : "min.insync.replicas",
       "valid_values" : "1~3",
       "default_value" : "1",
       "config_type" : "dynamic",
       "value" : "1",
       "value_type" : "integer"
     }, {
       "name" : "message.max.bytes",
       "valid_values" : "0~10485760",
       "default_value" : "10485760",
       "config_type" : "dynamic",
       "value" : "10485760",
       "value_type" : "integer"
     }, {
       "name" : "auto.create.groups.enable",
       "valid_values" : "true,false",
       "default_value" : "true",
       "config_type" : "dynamic",
       "value" : "true",
       "value_type" : "enum"
     }, {
       "name" : "connections.max.idle.ms",
       "valid_values" : "5000~600000",
       "default_value" : "600000",
       "config_type" : "static",
       "value" : "600000",
       "value_type" : "integer"
     }, {
       "name" : "log.retention.hours",
       "valid_values" : "1~168",
       "default_value" : "72",
       "config_type" : "static",
       "value" : "72",
       "value_type" : "integer"
     }, {
       "name" : "max.connections.per.ip",
       "valid_values" : "100~20000",
       "default_value" : "1000",
       "config_type" : "dynamic",
       "value" : "1000",
       "value_type" : "integer"
     }, {
       "name" : "group.max.session.timeout.ms",
       "valid_values" : "6000~1800000",
       "default_value" : "1800000",
       "config_type" : "static",
       "value" : "1800000",
       "value_type" : "integer"
     }, {
       "name" : "unclean.leader.election.enable",
       "valid_values" : "true,false",
       "default_value" : "false",
       "config_type" : "dynamic",
       "value" : "false",
       "value_type" : "enum"
     }, {
       "name" : "default.replication.factor",
       "valid_values" : "1~3",
       "default_value" : "3",
       "config_type" : "static",
       "value" : "3",
       "value_type" : "integer"
     }, {
       "name" : "offsets.retention.minutes",
       "valid_values" : "1440~30240",
       "default_value" : "20160",
       "config_type" : "dynamic",
       "value" : "20160",
       "value_type" : "integer"
     }, {
       "name" : "num.partitions",
       "valid_values" : "1~200",
       "default_value" : "3",
       "config_type" : "static",
       "value" : "3",
       "value_type" : "integer"
     }, {
       "name" : "group.min.session.timeout.ms",
       "valid_values" : "6000~300000",
       "default_value" : "6000",
       "config_type" : "static",
       "value" : "6000",
       "value_type" : "integer"
     }, {
       "name" : "allow.everyone.if.no.acl.found",
       "valid_values" : "true,false",
       "default_value" : "true",
       "config_type" : "static",
       "value" : "true",
       "value_type" : "enum"
     } ]
   }

Status Codes
------------

=========== =======================
Status Code Description
=========== =======================
200         Configuration obtained.
=========== =======================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
