:original_name: ModifyInstanceConfigs.html

.. _ModifyInstanceConfigs:

Modifying Instance Configurations
=================================

Function
--------

This API is used to modify instance configurations.

URI
---

PUT /v2/{project_id}/instances/{instance_id}/configs

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

.. table:: **Table 2** Request body parameters

   +---------------+-----------+----------------------------------------------------------------------------------------------------+--------------------------------+
   | Parameter     | Mandatory | Type                                                                                               | Description                    |
   +===============+===========+====================================================================================================+================================+
   | kafka_configs | No        | Array of :ref:`ModifyInstanceConfig <modifyinstanceconfigs__request_modifyinstanceconfig>` objects | Configurations to be modified. |
   +---------------+-----------+----------------------------------------------------------------------------------------------------+--------------------------------+

.. _modifyinstanceconfigs__request_modifyinstanceconfig:

.. table:: **Table 3** ModifyInstanceConfig

   ========= ========= ====== ========================================
   Parameter Mandatory Type   Description
   ========= ========= ====== ========================================
   name      No        String Names of configurations to be modified.
   value     No        String New value of the modified configuration.
   ========= ========= ====== ========================================

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   +----------------+---------+------------------------------------------------------------+
   | Parameter      | Type    | Description                                                |
   +================+=========+============================================================+
   | job_id         | String  | Configuration modification task ID.                        |
   +----------------+---------+------------------------------------------------------------+
   | dynamic_config | Integer | Number of dynamic configuration parameters to be modified. |
   +----------------+---------+------------------------------------------------------------+
   | static_config  | Integer | Number of static configuration parameters to be modified.  |
   +----------------+---------+------------------------------------------------------------+

Example Requests
----------------

Modifying the threshold for idle connection timeout and the log deletion interval.

.. code-block:: text

   PUT https://{endpoint}/v2/{project_id}/instances/{instance_id}/configs

   {
     "kafka_configs" : [ {
       "name" : "connections.max.idle.ms",
       "value" : "500000"
     }, {
       "name" : "log.retention.hours",
       "value" : "66"
     } ]
   }

Example Responses
-----------------

**Status code: 200**

Configuration modified.

.. code-block::

   {
     "job_id" : "8abfa7b38ba79a20018ba9afc550576a",
     "dynamic_config" : 0,
     "static_config" : 2
   }

Status Codes
------------

=========== =======================
Status Code Description
=========== =======================
200         Configuration modified.
=========== =======================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
