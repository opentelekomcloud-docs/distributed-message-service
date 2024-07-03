:original_name: ListEngineProducts.html

.. _ListEngineProducts:

Querying Product Specifications List
====================================

Function
--------

This API is used to query the product specifications list.

URI
---

GET /v2/{engine}/products

.. table:: **Table 1** Path Parameters

   +-----------------+-----------------+-----------------+--------------------+
   | Parameter       | Mandatory       | Type            | Description        |
   +=================+=================+=================+====================+
   | engine          | Yes             | String          | Message engine.    |
   |                 |                 |                 |                    |
   |                 |                 |                 | Default: **kafka** |
   +-----------------+-----------------+-----------------+--------------------+

.. table:: **Table 2** Query Parameters

   ========== ========= ====== ===========
   Parameter  Mandatory Type   Description
   ========== ========= ====== ===========
   product_id No        String Product ID.
   ========== ========= ====== ===========

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-----------+----------------------------------------------------------------------------------------------------------+--------------------------------+
   | Parameter | Type                                                                                                     | Description                    |
   +===========+==========================================================================================================+================================+
   | engine    | String                                                                                                   | Message engine of DMS.         |
   +-----------+----------------------------------------------------------------------------------------------------------+--------------------------------+
   | versions  | Array of strings                                                                                         | Supported versions.            |
   +-----------+----------------------------------------------------------------------------------------------------------+--------------------------------+
   | products  | Array of :ref:`ListEngineProductsEntity <listengineproducts__response_listengineproductsentity>` objects | Product specification details. |
   +-----------+----------------------------------------------------------------------------------------------------------+--------------------------------+

.. _listengineproducts__response_listengineproductsentity:

.. table:: **Table 4** ListEngineProductsEntity

   +------------------+------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | Parameter        | Type                                                                                                                   | Description                                                            |
   +==================+========================================================================================================================+========================================================================+
   | type             | String                                                                                                                 | Product type. Currently, single-node and cluster types are supported.  |
   +------------------+------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | product_id       | String                                                                                                                 | Product ID.                                                            |
   +------------------+------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | ecs_flavor_id    | String                                                                                                                 | ECS flavor.                                                            |
   +------------------+------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | arch_types       | Array of strings                                                                                                       | CPU architecture.                                                      |
   +------------------+------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | charging_mode    | Array of strings                                                                                                       | Billing mode. **hourly**: pay-per-use                                  |
   +------------------+------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | ios              | Array of :ref:`ListEngineIosEntity <listengineproducts__response_listengineiosentity>` objects                         | List of supported disk I/O types.                                      |
   +------------------+------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | support_features | Array of :ref:`ListEngineSupportFeaturesEntity <listengineproducts__response_listenginesupportfeaturesentity>` objects | List of features supported by instances of the current specifications. |
   +------------------+------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | properties       | :ref:`ListEnginePropertiesEntity <listengineproducts__response_listenginepropertiesentity>` object                     | Attribute of instances of the current specifications.                  |
   +------------------+------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------+

.. _listengineproducts__response_listengineiosentity:

.. table:: **Table 5** ListEngineIosEntity

   ================= ================ ================
   Parameter         Type             Description
   ================= ================ ================
   io_spec           String           Disk I/O code.
   type              String           Disk type.
   available_zones   Array of strings Available AZs.
   unavailable_zones Array of strings Unavailable AZs.
   ================= ================ ================

.. _listengineproducts__response_listenginesupportfeaturesentity:

.. table:: **Table 6** ListEngineSupportFeaturesEntity

   +------------+----------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------+
   | Parameter  | Type                                                                                                                             | Description                                            |
   +============+==================================================================================================================================+========================================================+
   | name       | String                                                                                                                           | Feature name.                                          |
   +------------+----------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------+
   | properties | :ref:`ListEngineSupportFeaturesPropertiesEntity <listengineproducts__response_listenginesupportfeaturespropertiesentity>` object | Description of the features supported by the instance. |
   +------------+----------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------+

.. _listengineproducts__response_listenginesupportfeaturespropertiesentity:

.. table:: **Table 7** ListEngineSupportFeaturesPropertiesEntity

   ========= ====== ================================
   Parameter Type   Description
   ========= ====== ================================
   max_task  String Maximum number of dumping tasks.
   min_task  String Minimum number of dumping tasks.
   max_node  String Maximum number of dumping nodes.
   min_node  String Minimum number of dumping nodes.
   ========= ====== ================================

.. _listengineproducts__response_listenginepropertiesentity:

.. table:: **Table 8** ListEnginePropertiesEntity

   +--------------------------+--------+-------------------------------------------------------+
   | Parameter                | Type   | Description                                           |
   +==========================+========+=======================================================+
   | max_partition_per_broker | String | Maximum number of partitions of each broker.          |
   +--------------------------+--------+-------------------------------------------------------+
   | max_broker               | String | Maximum number of brokers.                            |
   +--------------------------+--------+-------------------------------------------------------+
   | max_storage_per_node     | String | Maximum storage space of each broker. The unit is GB. |
   +--------------------------+--------+-------------------------------------------------------+
   | max_consumer_per_broker  | String | Maximum number of consumers of each broker.           |
   +--------------------------+--------+-------------------------------------------------------+
   | min_broker               | String | Minimum number of brokers.                            |
   +--------------------------+--------+-------------------------------------------------------+
   | max_bandwidth_per_broker | String | Maximum bandwidth of each broker.                     |
   +--------------------------+--------+-------------------------------------------------------+
   | min_storage_per_node     | String | Minimum storage space of each broker. The unit is GB. |
   +--------------------------+--------+-------------------------------------------------------+
   | max_tps_per_broker       | String | Maximum TPS of each broker.                           |
   +--------------------------+--------+-------------------------------------------------------+
   | product_alias            | String | Alias of **product_id**.                              |
   +--------------------------+--------+-------------------------------------------------------+

Example Requests
----------------

.. code-block:: text

   GET https://{endpoint}/v2/kafka/products

Example Responses
-----------------

**Status code: 200**

The product specifications are listed successfully.

.. code-block::

   {
     "engine" : "kafka",
     "versions" : [ "1.1.0", "2.3.0" ],
     "products" : [ {
       "type" : "cluster",
       "product_id" : "c6.2u4g.cluster",
       "ecs_flavor_id" : "c6.large.2",
       "billing_code" : "dms.platinum.c6",
       "arch_types" : [ "X86" ],
       "charging_mode" : [ "monthly", "hourly" ],
       "ios" : [ {
         "io_spec" : "dms.physical.storage.high.v2",
         "type" : "evs",
         "available_zones" : [ "xxx", "xxx" ],
         "unavailable_zones" : [ "xxx", "xxx" ]
       }, {
         "io_spec" : "dms.physical.storage.ultra.v2",
         "type" : "evs",
         "available_zones" : [ "xxx", "xxx" ],
         "unavailable_zones" : [ "xxx", "xxx" ]
       } ],
       "support_features" : [ {
         "name" : "connector_obs",
         "properties" : {
           "max_task" : "10",
           "max_node" : "10",
           "min_task" : "1",
           "min_node" : "2"
         }
       } ],
       "properties" : {
         "max_partition_per_broker" : "250",
         "max_broker" : "30",
         "max_storage_per_node" : "10000",
         "max_consumer_per_broker" : "4000",
         "min_broker" : "3",
         "max_bandwidth_per_broker" : "100",
         "min_storage_per_node" : "200",
         "max_tps_per_broker" : "30000",
         "product_alias" : "kafka.2u4g.cluster"
       }
     }, {
       "type" : "cluster",
       "product_id" : "c6.4u8g.cluster",
       "ecs_flavor_id" : "c6.xlarge.2",
       "billing_code" : "dms.platinum.c6",
       "arch_types" : [ "X86" ],
       "charging_mode" : [ "monthly", "hourly" ],
       "ios" : [ {
         "io_spec" : "dms.physical.storage.high.v2",
         "type" : "evs",
         "available_zones" : [ "xxx", "xxx" ],
         "unavailable_zones" : [ "xxx", "xxx" ]
       }, {
         "io_spec" : "dms.physical.storage.ultra.v2",
         "type" : "evs",
         "available_zones" : [ "xxx", "xxx" ],
         "unavailable_zones" : [ "xxx", "xxx" ]
       } ],
       "support_features" : [ {
         "name" : "connector_obs",
         "properties" : {
           "max_task" : "10",
           "max_node" : "10",
           "min_task" : "1",
           "min_node" : "2"
         }
       } ],
       "properties" : {
         "max_partition_per_broker" : "500",
         "max_broker" : "30",
         "max_storage_per_node" : "20000",
         "max_consumer_per_broker" : "4000",
         "min_broker" : "3",
         "max_bandwidth_per_broker" : "100",
         "min_storage_per_node" : "400",
         "max_tps_per_broker" : "100000",
         "product_alias" : "kafka.4u8g.cluster"
       }
     }, {
       "type" : "cluster",
       "product_id" : "c6.8u16g.cluster",
       "ecs_flavor_id" : "c6.2xlarge.2",
       "billing_code" : "dms.platinum.c6",
       "arch_types" : [ "X86" ],
       "charging_mode" : [ "monthly", "hourly" ],
       "ios" : [ {
         "io_spec" : "dms.physical.storage.high.v2",
         "type" : "evs",
         "available_zones" : [ "xxx", "xxx" ],
         "unavailable_zones" : [ "xxx", "xxx" ]
       }, {
         "io_spec" : "dms.physical.storage.ultra.v2",
         "type" : "evs",
         "available_zones" : [ "xxx", "xxx" ],
         "unavailable_zones" : [ "xxx", "xxx" ]
       } ],
       "support_features" : [ {
         "name" : "connector_obs",
         "properties" : {
           "max_task" : "10",
           "max_node" : "10",
           "min_task" : "1",
           "min_node" : "2"
         }
       } ],
       "properties" : {
         "max_partition_per_broker" : "1000",
         "max_broker" : "30",
         "max_storage_per_node" : "30000",
         "max_consumer_per_broker" : "4000",
         "min_broker" : "3",
         "max_bandwidth_per_broker" : "100",
         "min_storage_per_node" : "800",
         "max_tps_per_broker" : "150000",
         "product_alias" : "kafka.8u16g.cluster"
       }
     }, {
       "type" : "cluster",
       "product_id" : "c6.12u24g.cluster",
       "ecs_flavor_id" : "c6.3xlarge.2",
       "billing_code" : "dms.platinum.c6",
       "arch_types" : [ "X86" ],
       "charging_mode" : [ "monthly", "hourly" ],
       "ios" : [ {
         "io_spec" : "dms.physical.storage.high.v2",
         "type" : "evs",
         "available_zones" : [ "xxx", "xxx" ],
         "unavailable_zones" : [ "xxx", "xxx" ]
       }, {
         "io_spec" : "dms.physical.storage.ultra.v2",
         "type" : "evs",
         "available_zones" : [ "xxx", "xxx" ],
         "unavailable_zones" : [ "xxx", "xxx" ]
       } ],
       "support_features" : [ {
         "name" : "connector_obs",
         "properties" : {
           "max_task" : "10",
           "max_node" : "10",
           "min_task" : "1",
           "min_node" : "2"
         }
       } ],
       "properties" : {
         "max_partition_per_broker" : "1500",
         "max_broker" : "30",
         "max_storage_per_node" : "30000",
         "max_consumer_per_broker" : "4000",
         "min_broker" : "3",
         "max_bandwidth_per_broker" : "100",
         "min_storage_per_node" : "1200",
         "max_tps_per_broker" : "200000",
         "product_alias" : "kafka.12u24g.cluster"
       }
     }, {
       "type" : "cluster",
       "product_id" : "c6.16u32g.cluster",
       "ecs_flavor_id" : "c6.4xlarge.2",
       "billing_code" : "dms.platinum.c6",
       "arch_types" : [ "X86" ],
       "charging_mode" : [ "monthly", "hourly" ],
       "ios" : [ {
         "io_spec" : "dms.physical.storage.high.v2",
         "type" : "evs",
         "available_zones" : [ "xxx", "xxx" ],
         "unavailable_zones" : [ "xxx", "xxx" ]
       }, {
         "io_spec" : "dms.physical.storage.ultra.v2",
         "type" : "evs",
         "available_zones" : [ "xxx", "xxx" ],
         "unavailable_zones" : [ "xxx", "xxx" ]
       } ],
       "support_features" : [ {
         "name" : "connector_obs",
         "properties" : {
           "max_task" : "10",
           "max_node" : "10",
           "min_task" : "1",
           "min_node" : "2"
         }
       } ],
       "properties" : {
         "max_partition_per_broker" : "2000",
         "max_broker" : "30",
         "max_storage_per_node" : "30000",
         "max_consumer_per_broker" : "4000",
         "min_broker" : "3",
         "max_bandwidth_per_broker" : "100",
         "min_storage_per_node" : "1600",
         "max_tps_per_broker" : "250000",
         "product_alias" : "kafka.16u32g.cluster"
       }
     } ]
   }

Status Codes
------------

=========== ===================================================
Status Code Description
=========== ===================================================
200         The product specifications are listed successfully.
=========== ===================================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
