:original_name: ShowEngineInstanceExtendProductInfo.html

.. _ShowEngineInstanceExtendProductInfo:

Querying Product Information for Instance Specification Modification
====================================================================

Function
--------

This API is used to query the product information for instance specification modification.

URI
---

GET /v2/{engine}/{project_id}/instances/{instance_id}/extend

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                                               |
   +=============+===========+========+===========================================================================================================+
   | engine      | Yes       | String | Message engine.                                                                                           |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | project_id  | Yes       | String | Project ID. For details about how to obtain it, see :ref:`Obtaining a Project ID <kafka-api-0036212547>`. |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                                              |
   +-------------+-----------+--------+-----------------------------------------------------------------------------------------------------------+

.. table:: **Table 2** Query Parameters

   +-----------------+-----------------+-----------------+----------------------------------+
   | Parameter       | Mandatory       | Type            | Description                      |
   +=================+=================+=================+==================================+
   | type            | Yes             | String          | Product edition.                 |
   |                 |                 |                 |                                  |
   |                 |                 |                 | -  **advanced**: premium edition |
   +-----------------+-----------------+-----------------+----------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-----------+-------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------+
   | Parameter | Type                                                                                                                    | Description                                         |
   +===========+=========================================================================================================================+=====================================================+
   | engine    | String                                                                                                                  | Message engine: Kafka.                              |
   +-----------+-------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------+
   | versions  | Array of strings                                                                                                        | Versions supported by the message engine.           |
   +-----------+-------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------+
   | products  | Array of :ref:`ExtendProductInfoEntity <showengineinstanceextendproductinfo__response_extendproductinfoentity>` objects | Product information for specification modification. |
   +-----------+-------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------+

.. _showengineinstanceextendproductinfo__response_extendproductinfoentity:

.. table:: **Table 4** ExtendProductInfoEntity

   +-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
   | Parameter         | Type                                                                                                                                          | Description                              |
   +===================+===============================================================================================================================================+==========================================+
   | type              | String                                                                                                                                        | Instance type.                           |
   +-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
   | product_id        | String                                                                                                                                        | Product ID.                              |
   +-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
   | ecs_flavor_id     | String                                                                                                                                        | ECS flavor used by the product.          |
   +-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
   | arch_types        | Array of strings                                                                                                                              | Supported CPU architectures.             |
   +-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
   | charging_mode     | Array of strings                                                                                                                              | Supported billing modes.                 |
   +-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
   | ios               | Array of :ref:`ExtendProductIosEntity <showengineinstanceextendproductinfo__response_extendproductiosentity>` objects                         | Disk I/O information.                    |
   +-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
   | support_features  | Array of :ref:`ExtendProductSupportFeaturesEntity <showengineinstanceextendproductinfo__response_extendproductsupportfeaturesentity>` objects | Supported features.                      |
   +-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
   | properties        | :ref:`ExtendProductPropertiesEntity <showengineinstanceextendproductinfo__response_extendproductpropertiesentity>` object                     | Product specification description.       |
   +-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
   | available_zones   | Array of strings                                                                                                                              | AZs where there are available resources. |
   +-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
   | unavailable_zones | Array of strings                                                                                                                              | AZs where resources are sold out.        |
   +-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+

.. _showengineinstanceextendproductinfo__response_extendproductiosentity:

.. table:: **Table 5** ExtendProductIosEntity

   +-------------------+------------------+------------------------------------------+
   | Parameter         | Type             | Description                              |
   +===================+==================+==========================================+
   | io_spec           | String           | Storage I/O specification.               |
   +-------------------+------------------+------------------------------------------+
   | available_zones   | Array of strings | AZs where there are available resources. |
   +-------------------+------------------+------------------------------------------+
   | type              | String           | I/O type.                                |
   +-------------------+------------------+------------------------------------------+
   | unavailable_zones | Array of strings | AZs where resources are sold out.        |
   +-------------------+------------------+------------------------------------------+

.. _showengineinstanceextendproductinfo__response_extendproductsupportfeaturesentity:

.. table:: **Table 6** ExtendProductSupportFeaturesEntity

   ========== ================== ============================
   Parameter  Type               Description
   ========== ================== ============================
   name       String             Feature name.
   properties Map<String,String> Key-value pair of a feature.
   ========== ================== ============================

.. _showengineinstanceextendproductinfo__response_extendproductpropertiesentity:

.. table:: **Table 7** ExtendProductPropertiesEntity

   +--------------------------+--------+-------------------------------------------------+
   | Parameter                | Type   | Description                                     |
   +==========================+========+=================================================+
   | max_partition_per_broker | String | Maximum number of partitions of each broker.    |
   +--------------------------+--------+-------------------------------------------------+
   | max_broker               | String | Maximum number of brokers.                      |
   +--------------------------+--------+-------------------------------------------------+
   | max_storage_per_node     | String | Maximum storage space of each broker. Unit: GB. |
   +--------------------------+--------+-------------------------------------------------+
   | max_consumer_per_broker  | String | Maximum number of consumers of each broker.     |
   +--------------------------+--------+-------------------------------------------------+
   | min_broker               | String | Minimum number of brokers.                      |
   +--------------------------+--------+-------------------------------------------------+
   | max_bandwidth_per_broker | String | Maximum bandwidth of each broker.               |
   +--------------------------+--------+-------------------------------------------------+
   | min_storage_per_node     | String | Minimum storage space of each broker. Unit: GB. |
   +--------------------------+--------+-------------------------------------------------+
   | max_tps_per_broker       | String | Maximum TPS of each broker.                     |
   +--------------------------+--------+-------------------------------------------------+
   | product_alias            | String | Alias of **product_id**.                        |
   +--------------------------+--------+-------------------------------------------------+

Example Requests
----------------

Querying product information for instance specification modification

.. code-block:: text

   GET https://{endpoint}/v2/{engine}/{project_id}/instances/{instance_id}/extend?type={type}

Example Responses
-----------------

**Status code: 200**

Successfully queried the product information for instance specification modification.

-  Product information for instance specification modification queried.

   .. code-block::

      {
        "engine" : "kafka",
        "versions" : [ "1.1.0", "2.7" ],
        "products" : [ {
          "type" : "cluster",
          "product_id" : "c6.2u4g.cluster",
          "ecs_flavor_id" : "c3.large.2",
          "arch_types" : [ "X86" ],
          "charging_mode" : [ "monthly", "hourly" ],
          "ios" : [ {
            "io_spec" : "dms.physical.storage.high.v2",
            "available_zones" : [ "xxx" ],
            "type" : "evs",
            "unavailable_zones" : [ ]
          }, {
            "io_spec" : "dms.physical.storage.ultra.v2",
            "available_zones" : [ "xxx" ],
            "type" : "evs",
            "unavailable_zones" : [ ]
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
            "product_alias" : "kafka.2u4g.cluster",
            "max_bandwidth_per_broker" : "100",
            "min_storage_per_node" : "100",
            "max_tps_per_broker" : "30000"
          },
          "available_zones" : [ "xxx" ],
          "unavailable_zones" : [ ]
        }, {
          "type" : "cluster",
          "product_id" : "c6.2u4g.cluster.dec",
          "ecs_flavor_id" : "c6.large.2",
          "arch_types" : [ "X86" ],
          "charging_mode" : [ "monthly", "hourly" ],
          "ios" : [ {
            "io_spec" : "dms.physical.storage.high.dss.v2",
            "available_zones" : [ "xxx" ],
            "type" : "evs",
            "unavailable_zones" : [ ]
          }, {
            "io_spec" : "dms.physical.storage.ultra.dss.v2",
            "available_zones" : [ "xxx" ],
            "type" : "evs",
            "unavailable_zones" : [ ]
          }, {
            "io_spec" : "dms.physical.storage.ultra.v2",
            "available_zones" : [ "xxx" ],
            "type" : "evs",
            "unavailable_zones" : [ ]
          }, {
            "io_spec" : "dms.physical.storage.high.v2",
            "available_zones" : [ "xxx" ],
            "type" : "evs",
            "unavailable_zones" : [ ]
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
            "max_partition_per_broker" : "100",
            "max_broker" : "30",
            "max_storage_per_node" : "400",
            "max_consumer_per_broker" : "4000",
            "min_broker" : "3",
            "product_alias" : "kafka.2u4g.cluster.dec",
            "max_bandwidth_per_broker" : "100",
            "min_storage_per_node" : "100",
            "max_tps_per_broker" : "30000"
          },
          "available_zones" : [ ],
          "unavailable_zones" : [ "xxx" ]
        }, {
          "type" : "cluster",
          "product_id" : "c6.4u8g.cluster",
          "ecs_flavor_id" : "c3.xlarge.2",
          "arch_types" : [ "X86" ],
          "charging_mode" : [ "monthly", "hourly" ],
          "ios" : [ {
            "io_spec" : "dms.physical.storage.high.v2",
            "available_zones" : [ "xxx" ],
            "type" : "evs",
            "unavailable_zones" : [ ]
          }, {
            "io_spec" : "dms.physical.storage.ultra.v2",
            "available_zones" : [ "xxx" ],
            "type" : "evs",
            "unavailable_zones" : [ ]
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
            "product_alias" : "kafka.4u8g.cluster",
            "max_bandwidth_per_broker" : "100",
            "min_storage_per_node" : "100",
            "max_tps_per_broker" : "100000"
          },
          "available_zones" : [ "xxx" ],
          "unavailable_zones" : [ ]
        }, {
          "type" : "cluster",
          "product_id" : "c6.8u16g.cluster",
          "ecs_flavor_id" : "c3.2xlarge.2",
          "arch_types" : [ "X86" ],
          "charging_mode" : [ "monthly", "hourly" ],
          "ios" : [ {
            "io_spec" : "dms.physical.storage.high.v2",
            "available_zones" : [ "xxx" ],
            "type" : "evs",
            "unavailable_zones" : [ ]
          }, {
            "io_spec" : "dms.physical.storage.ultra.v2",
            "available_zones" : [ "xxx" ],
            "type" : "evs",
            "unavailable_zones" : [ ]
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
            "product_alias" : "kafka.8u16g.cluster",
            "max_bandwidth_per_broker" : "100",
            "min_storage_per_node" : "100",
            "max_tps_per_broker" : "150000"
          },
          "available_zones" : [ "xxx" ],
          "unavailable_zones" : [ ]
        }, {
          "type" : "cluster",
          "product_id" : "c6.12u24g.cluster",
          "ecs_flavor_id" : "c3.3xlarge.2",
          "arch_types" : [ "X86" ],
          "charging_mode" : [ "monthly", "hourly" ],
          "ios" : [ {
            "io_spec" : "dms.physical.storage.high.v2",
            "available_zones" : [ "xxx" ],
            "type" : "evs",
            "unavailable_zones" : [ ]
          }, {
            "io_spec" : "dms.physical.storage.ultra.v2",
            "available_zones" : [ "xxx" ],
            "type" : "evs",
            "unavailable_zones" : [ ]
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
            "product_alias" : "kafka.12u24g.cluster",
            "max_bandwidth_per_broker" : "100",
            "min_storage_per_node" : "100",
            "max_tps_per_broker" : "200000"
          },
          "available_zones" : [ "xxx" ],
          "unavailable_zones" : [ ]
        }, {
          "type" : "cluster",
          "product_id" : "c6.16u32g.cluster",
          "ecs_flavor_id" : "c3.4xlarge.2",
          "arch_types" : [ "X86" ],
          "charging_mode" : [ "monthly", "hourly" ],
          "ios" : [ {
            "io_spec" : "dms.physical.storage.high.v2",
            "available_zones" : [ "xxx" ],
            "type" : "evs",
            "unavailable_zones" : [ ]
          }, {
            "io_spec" : "dms.physical.storage.ultra.v2",
            "available_zones" : [ "xxx" ],
            "type" : "evs",
            "unavailable_zones" : [ ]
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
            "product_alias" : "kafka.16u32g.cluster",
            "max_bandwidth_per_broker" : "100",
            "min_storage_per_node" : "100",
            "max_tps_per_broker" : "250000"
          },
          "available_zones" : [ "xxx" ],
          "unavailable_zones" : [ ]
        } ]
      }

Status Codes
------------

+-------------+---------------------------------------------------------------------------------------+
| Status Code | Description                                                                           |
+=============+=======================================================================================+
| 200         | Successfully queried the product information for instance specification modification. |
+-------------+---------------------------------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
