:original_name: kafka-api-180514009.html

.. _kafka-api-180514009:

Querying Product Specifications
===============================

.. note::

   This API is out-of-date and may not be maintained in the future.

Function
--------

This API is used to query the product specifications to configure the product ID.

URI
---

GET /v1.0/products?engine={engine}

:ref:`Table 1 <kafka-api-180514009__en-us_topic_0128036912_table0211262515>` describes the parameter.

.. _kafka-api-180514009__en-us_topic_0128036912_table0211262515:

.. table:: **Table 1** Parameters

   ========= ====== ========= =============================
   Parameter Type   Mandatory Description
   ========= ====== ========= =============================
   engine    String Yes       Indicates the message engine.
   ========= ====== ========= =============================

Request
-------

**Request parameters**

None.

**Example request**

.. code-block:: text

   GET https://{dms_endpoint}/v1.0/products?engine={engine}

Response
--------

**Response parameters**

:ref:`Table 2 <kafka-api-180514009__en-us_topic_0128036912_table18238145151512>` describes the response parameters.

.. _kafka-api-180514009__en-us_topic_0128036912_table18238145151512:

.. table:: **Table 2** Parameters

   +-----------+--------+-------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Type   | Description                                                                                                                         |
   +===========+========+=====================================================================================================================================+
   | name      | String | Indicates the message engine, which is **kafka**.                                                                                   |
   +-----------+--------+-------------------------------------------------------------------------------------------------------------------------------------+
   | version   | String | Indicates the version of the message engine. Currently, only 1.1.0 and 2.3.0 are supported.                                         |
   +-----------+--------+-------------------------------------------------------------------------------------------------------------------------------------+
   | values    | Array  | Indicates product specifications. For details, see :ref:`Table 3 <kafka-api-180514009__en-us_topic_0128036912_table1380164413184>`. |
   +-----------+--------+-------------------------------------------------------------------------------------------------------------------------------------+

.. _kafka-api-180514009__en-us_topic_0128036912_table1380164413184:

.. table:: **Table 3** values parameter description

   +-------------------+--------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter         | Type   | Description                                                                                                                               |
   +===================+========+===========================================================================================================================================+
   | detail            | Array  | Indicates the details of specifications. For details, see :ref:`Table 4 <kafka-api-180514009__en-us_topic_0128036912_table131863331362>`. |
   +-------------------+--------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | name              | String | Indicates the instance type.                                                                                                              |
   +-------------------+--------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | unavailable_zones | Array  | Indicates AZs where resources are sold out.                                                                                               |
   +-------------------+--------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | available_zones   | Array  | Indicates AZs where there are available resources.                                                                                        |
   +-------------------+--------+-------------------------------------------------------------------------------------------------------------------------------------------+

.. _kafka-api-180514009__en-us_topic_0128036912_table131863331362:

.. table:: **Table 4** detail parameter description

   +-----------------+--------+----------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type   | Description                                                                                                                      |
   +=================+========+==================================================================================================================================+
   | tps             | String | Indicates the maximum number of messages per unit time.                                                                          |
   +-----------------+--------+----------------------------------------------------------------------------------------------------------------------------------+
   | storage         | String | Indicates the message storage space.                                                                                             |
   +-----------------+--------+----------------------------------------------------------------------------------------------------------------------------------+
   | partition_num   | String | Indicates the maximum number of topics in a Kafka instance.                                                                      |
   +-----------------+--------+----------------------------------------------------------------------------------------------------------------------------------+
   | product_id      | String | Indicates the product ID.                                                                                                        |
   +-----------------+--------+----------------------------------------------------------------------------------------------------------------------------------+
   | spec_code       | String | Indicates the specification ID.                                                                                                  |
   +-----------------+--------+----------------------------------------------------------------------------------------------------------------------------------+
   | io              | Array  | Indicates the I/O information. For details, see :ref:`Table 5 <kafka-api-180514009__en-us_topic_0128036912_table1132314152265>`. |
   +-----------------+--------+----------------------------------------------------------------------------------------------------------------------------------+
   | bandwidth       | String | Indicates the bandwidth of a Kafka instance.                                                                                     |
   +-----------------+--------+----------------------------------------------------------------------------------------------------------------------------------+
   | available_zones | Array  | Indicates AZs where there are available resources.                                                                               |
   +-----------------+--------+----------------------------------------------------------------------------------------------------------------------------------+
   | ecs_flavor_id   | String | Indicates the flavors of the corresponding ECS.                                                                                  |
   +-----------------+--------+----------------------------------------------------------------------------------------------------------------------------------+
   | arch_type       | String | Indicates the instance architecture type. Currently, only x86 is supported.                                                      |
   +-----------------+--------+----------------------------------------------------------------------------------------------------------------------------------+

.. _kafka-api-180514009__en-us_topic_0128036912_table1132314152265:

.. table:: **Table 5** io parameter description

   +-------------------+------------------+--------------------------------------------------------+
   | Parameter         | Type             | Description                                            |
   +===================+==================+========================================================+
   | io_type           | String           | Indicates the I/O type.                                |
   +-------------------+------------------+--------------------------------------------------------+
   | storage_spec_code | String           | Indicates the I/O specification.                       |
   +-------------------+------------------+--------------------------------------------------------+
   | available_zones   | Array            | Indicates AZs where there are available I/O resources. |
   +-------------------+------------------+--------------------------------------------------------+
   | unavailable_zones | Array of strings | Indicates AZs where I/O resources are sold out.        |
   +-------------------+------------------+--------------------------------------------------------+
   | volume_type       | String           | Indicates the disk type.                               |
   +-------------------+------------------+--------------------------------------------------------+

**Example response**

.. code-block::

   {
       "Hourly": [{
           "name": "kafka",
           "version": "2.3.0",
           "values": [{
               "detail": [{
                   "tps": "50000",
                   "storage": "600",
                   "partition_num": "300",
                   "product_id": "00300-30308-0--0",
                   "spec_code": "dms.instance.kafka.cluster.c3.mini",
                   "io": [{
                       "io_type": "high",
                       "storage_spec_code": "dms.physical.storage.high",
                       "available_zones": ["XXX",
                       "XXX"],
                       "volume_type": "SAS"
                   },
                   {
                       "io_type": "ultra",
                       "storage_spec_code": "dms.physical.storage.ultra",
                       "available_zones": ["XXX",
                       "XXX"],
                       "volume_type": "SSD"
                   }],
                   "bandwidth": "100MB",
                   "unavailable_zones": ["XXX"],
                   "available_zones": ["XXX"],
                   "ecs_flavor_id": "c4.large.2",
                   "arch_type": "X86"
               },
               {
                   "tps": "100000",
                   "storage": "1200",
                   "partition_num": "900",
                   "product_id": "00300-30310-0--0",
                   "spec_code": "dms.instance.kafka.cluster.c3.small.2",
                   "io": [{
                       "io_type": "high",
                       "storage_spec_code": "dms.physical.storage.high",
                       "available_zones": ["XXX",
                       "XXX"],
                       "volume_type": "SAS"
                   },
                   {
                       "io_type": "ultra",
                       "storage_spec_code": "dms.physical.storage.ultra",
                       "available_zones": ["XXX",
                       "XXX"],
                       "volume_type": "SSD"
                   }],
                   "bandwidth": "300MB",
                   "unavailable_zones": ["XXX"],
                   "available_zones": ["XXX"],
                   "ecs_flavor_id": "c4.xlarge.2",
                   "arch_type": "X86"
               },
               {
                   "tps": "200000",
                   "storage": "2400",
                   "partition_num": "1800",
                   "product_id": "00300-30312-0--0",
                   "spec_code": "dms.instance.kafka.cluster.c3.middle.2",
                   "io": [{
                       "io_type": "ultra",
                       "storage_spec_code": "dms.physical.storage.ultra",
                       "available_zones": ["XXX",
                       "XXX"],
                       "volume_type": "SSD"
                   }],
                   "bandwidth": "600MB",
                   "unavailable_zones": ["XXX"],
                   "available_zones": ["XXX"],
                   "ecs_flavor_id": "c4.2xlarge.2",
                   "arch_type": "X86"
               },
               {
                   "tps": "300000",
                   "storage": "4800",
                   "partition_num": "1800",
                   "product_id": "00300-30314-0--0",
                   "spec_code": "dms.instance.kafka.cluster.c3.high.2",
                   "io": [{
                       "io_type": "ultra",
                       "storage_spec_code": "dms.physical.storage.ultra",
                       "available_zones": ["XXX",
                       "XXX"],
                       "volume_type": "SSD"
                   }],
                   "bandwidth": "1200MB",
                   "unavailable_zones": ["XXX"],
                   "available_zones": ["XXX"],
                   "ecs_flavor_id": "c4.2xlarge.2",
                   "arch_type": "X86"
               }],
               "name": "cluster",
               "unavailable_zones": ["XXX"],
               "available_zones": ["XXX"]
           }]
       }]
   }

Status Code
-----------

:ref:`Table 6 <kafka-api-180514009__en-us_topic_0128036912_table2557155375912>` describes the status code of successful operations. For details about other status codes, see :ref:`Status Code <kafka-api-0034672261>`.

.. _kafka-api-180514009__en-us_topic_0128036912_table2557155375912:

.. table:: **Table 6** Status code

   =========== ============================================
   Status Code Description
   =========== ============================================
   200         Product specifications queried successfully.
   =========== ============================================
