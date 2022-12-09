:original_name: ListProducts_0.html

.. _ListProducts_0:

Listing Product Specifications
==============================

Function
--------

This API is used to query the product specifications to configure the product ID (**product_id**).For example, to create a pay-per-use Kafka instance with 100 MB/s bandwidth, locate the section where the value of **bandwidth** is **100MB** under "Hourly" in the response message. Then, the value of **product_id** in the same section is the product ID that should be configured for the Kafka instance.\ **unavailable_zones** indicates AZs where there are no available resources. If the value is empty, all AZs are available. Otherwise, the AZs listed in the value do not have sufficient resources. Ensure that the AZs where you want to create the instance are not listed here.

URI
---

GET /v2/products

.. table:: **Table 1** Query Parameters

   +-----------+-----------+--------+-----------------------------------------------------+
   | Parameter | Mandatory | Type   | Description                                         |
   +===========+===========+========+=====================================================+
   | engine    | Yes       | String | Message engine. Currently, only Kafka is supported. |
   +-----------+-----------+--------+-----------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameters

   +-----------+--------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Type                                                               | Description                                                                                                                   |
   +===========+====================================================================+===============================================================================================================================+
   | Hourly    | Array of :ref:`Hourly <listproducts_0__response_hourly>` objects   | List of pay-per-use products.                                                                                                 |
   +-----------+--------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
   | Monthly   | Array of :ref:`Monthly <listproducts_0__response_monthly>` objects | List of products in yearly/monthly billing mode. Currently, you cannot create yearly/monthly Kafka instances by calling APIs. |
   +-----------+--------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+

.. _listproducts_0__response_hourly:

.. table:: **Table 3** Hourly

   +-----------+------------------------------------------------------------------+------------------------------------------------------------------------------+
   | Parameter | Type                                                             | Description                                                                  |
   +===========+==================================================================+==============================================================================+
   | name      | String                                                           | Message engine, which is **kafka**.                                          |
   +-----------+------------------------------------------------------------------+------------------------------------------------------------------------------+
   | version   | String                                                           | Version of the message engine. Currently, only 1.1.0 and 2.3.0 is supported. |
   +-----------+------------------------------------------------------------------+------------------------------------------------------------------------------+
   | values    | Array of :ref:`values <listproducts_0__response_values>` objects | Product specifications.                                                      |
   +-----------+------------------------------------------------------------------+------------------------------------------------------------------------------+

.. _listproducts_0__response_values:

.. table:: **Table 4** values

   +-------------------+------------------------------------------------------------------+--------------------------------------------------+
   | Parameter         | Type                                                             | Description                                      |
   +===================+==================================================================+==================================================+
   | detail            | Array of :ref:`detail <listproducts_0__response_detail>` objects | Specification details.                           |
   +-------------------+------------------------------------------------------------------+--------------------------------------------------+
   | name              | String                                                           | Instance type.                                   |
   +-------------------+------------------------------------------------------------------+--------------------------------------------------+
   | unavailable_zones | Array of strings                                                 | AZs where resources are sold out.                |
   +-------------------+------------------------------------------------------------------+--------------------------------------------------+
   | available_zones   | Array of strings                                                 | List of AZs where there are available resources. |
   +-------------------+------------------------------------------------------------------+--------------------------------------------------+

.. _listproducts_0__response_detail:

.. table:: **Table 5** detail

   +-------------------+----------------------------------------------------------+---------------------------------------------------------------+
   | Parameter         | Type                                                     | Description                                                   |
   +===================+==========================================================+===============================================================+
   | tps               | String                                                   | Maximum number of messages per unit time.                     |
   +-------------------+----------------------------------------------------------+---------------------------------------------------------------+
   | storage_space     | String                                                   | Message storage space.                                        |
   +-------------------+----------------------------------------------------------+---------------------------------------------------------------+
   | partition_num     | String                                                   | Number of partitions in a Kafka instance.                     |
   +-------------------+----------------------------------------------------------+---------------------------------------------------------------+
   | product_id        | String                                                   | Product ID.                                                   |
   +-------------------+----------------------------------------------------------+---------------------------------------------------------------+
   | spec_code         | String                                                   | Specification ID.                                             |
   +-------------------+----------------------------------------------------------+---------------------------------------------------------------+
   | io                | Array of :ref:`io <listproducts_0__response_io>` objects | I/O information.                                              |
   +-------------------+----------------------------------------------------------+---------------------------------------------------------------+
   | bandwidth         | String                                                   | Bandwidth of a Kafka instance.                                |
   +-------------------+----------------------------------------------------------+---------------------------------------------------------------+
   | unavailable_zones | Array of strings                                         | AZs where resources are sold out.                             |
   +-------------------+----------------------------------------------------------+---------------------------------------------------------------+
   | available_zones   | Array of strings                                         | List of AZs where there are available resources.              |
   +-------------------+----------------------------------------------------------+---------------------------------------------------------------+
   | ecs_flavor_id     | String                                                   | Flavor of the corresponding ECS.                              |
   +-------------------+----------------------------------------------------------+---------------------------------------------------------------+
   | arch_type         | String                                                   | Instance architecture type. Currently, only x86 is supported. |
   +-------------------+----------------------------------------------------------+---------------------------------------------------------------+

.. _listproducts_0__response_io:

.. table:: **Table 6** io

   +-------------------+------------------+------------------------------------------------------+
   | Parameter         | Type             | Description                                          |
   +===================+==================+======================================================+
   | io_type           | String           | I/O type.                                            |
   +-------------------+------------------+------------------------------------------------------+
   | storage_spec_code | String           | I/O specifications.                                  |
   +-------------------+------------------+------------------------------------------------------+
   | available_zones   | Array of strings | List of AZs where there are available I/O resources. |
   +-------------------+------------------+------------------------------------------------------+
   | unavailable_zones | Array of strings | List of AZs where I/O resources are sold out.        |
   +-------------------+------------------+------------------------------------------------------+
   | volume_type       | String           | Disk type.                                           |
   +-------------------+------------------+------------------------------------------------------+

.. _listproducts_0__response_monthly:

.. table:: **Table 7** Monthly

   +-----------+--------------------------------------------------------------------+------------------------------------------------------------------------------+
   | Parameter | Type                                                               | Description                                                                  |
   +===========+====================================================================+==============================================================================+
   | name      | String                                                             | Message engine, which is **kafka**.                                          |
   +-----------+--------------------------------------------------------------------+------------------------------------------------------------------------------+
   | version   | String                                                             | Version of the message engine. Currently, only 1.1.0 and 2.3.0 is supported. |
   +-----------+--------------------------------------------------------------------+------------------------------------------------------------------------------+
   | values    | Array of :ref:`values <listproducts_0__response_values_1>` objects | Product specifications.                                                      |
   +-----------+--------------------------------------------------------------------+------------------------------------------------------------------------------+

.. _listproducts_0__response_values_1:

.. table:: **Table 8** values

   +-------------------+--------------------------------------------------------------------+--------------------------------------------------+
   | Parameter         | Type                                                               | Description                                      |
   +===================+====================================================================+==================================================+
   | detail            | Array of :ref:`detail <listproducts_0__response_detail_1>` objects | Specification details.                           |
   +-------------------+--------------------------------------------------------------------+--------------------------------------------------+
   | name              | String                                                             | Instance type.                                   |
   +-------------------+--------------------------------------------------------------------+--------------------------------------------------+
   | unavailable_zones | Array of strings                                                   | AZs where resources are sold out.                |
   +-------------------+--------------------------------------------------------------------+--------------------------------------------------+
   | available_zones   | Array of strings                                                   | List of AZs where there are available resources. |
   +-------------------+--------------------------------------------------------------------+--------------------------------------------------+

.. _listproducts_0__response_detail_1:

.. table:: **Table 9** detail

   +-------------------+------------------------------------------------------------+---------------------------------------------------------------+
   | Parameter         | Type                                                       | Description                                                   |
   +===================+============================================================+===============================================================+
   | tps               | String                                                     | Maximum number of messages per unit time.                     |
   +-------------------+------------------------------------------------------------+---------------------------------------------------------------+
   | storage_space     | String                                                     | Message storage space.                                        |
   +-------------------+------------------------------------------------------------+---------------------------------------------------------------+
   | partition_num     | String                                                     | Number of partitions in a Kafka instance.                     |
   +-------------------+------------------------------------------------------------+---------------------------------------------------------------+
   | product_id        | String                                                     | Product ID.                                                   |
   +-------------------+------------------------------------------------------------+---------------------------------------------------------------+
   | spec_code         | String                                                     | Specification ID.                                             |
   +-------------------+------------------------------------------------------------+---------------------------------------------------------------+
   | io                | Array of :ref:`io <listproducts_0__response_io_1>` objects | I/O information.                                              |
   +-------------------+------------------------------------------------------------+---------------------------------------------------------------+
   | bandwidth         | String                                                     | Bandwidth of a Kafka instance.                                |
   +-------------------+------------------------------------------------------------+---------------------------------------------------------------+
   | unavailable_zones | Array of strings                                           | AZs where resources are sold out.                             |
   +-------------------+------------------------------------------------------------+---------------------------------------------------------------+
   | available_zones   | Array of strings                                           | List of AZs where there are available resources.              |
   +-------------------+------------------------------------------------------------+---------------------------------------------------------------+
   | ecs_flavor_id     | String                                                     | Flavor of the corresponding ECS.                              |
   +-------------------+------------------------------------------------------------+---------------------------------------------------------------+
   | arch_type         | String                                                     | Instance architecture type. Currently, only x86 is supported. |
   +-------------------+------------------------------------------------------------+---------------------------------------------------------------+

.. _listproducts_0__response_io_1:

.. table:: **Table 10** io

   +-------------------+------------------+------------------------------------------------------+
   | Parameter         | Type             | Description                                          |
   +===================+==================+======================================================+
   | io_type           | String           | I/O type.                                            |
   +-------------------+------------------+------------------------------------------------------+
   | storage_spec_code | String           | I/O specifications.                                  |
   +-------------------+------------------+------------------------------------------------------+
   | available_zones   | Array of strings | List of AZs where there are available I/O resources. |
   +-------------------+------------------+------------------------------------------------------+
   | unavailable_zones | Array of strings | List of AZs where I/O resources are sold out.        |
   +-------------------+------------------+------------------------------------------------------+
   | volume_type       | String           | Disk type.                                           |
   +-------------------+------------------+------------------------------------------------------+

Example Requests
----------------

.. code-block:: text

   GET https://{endpoint}/v2/products?engine=kafka

Example Responses
-----------------

**Status code: 200**

The product specifications are listed successfully.

.. code-block::

   {
     "Hourly" : [ {
       "name" : "kafka",
       "version" : "1.1.0",
       "values" : [ {
         "detail" : [ {
           "tps" : "50000",
           "storage_space" : "200",
           "partition_num" : "300",
           "product_id" : "00300-30308-0--0",
           "spec_code" : "dms.instance.kafka.cluster.c3.mini",
           "io" : [ {
             "io_type" : "normal",
             "storage_spec_code" : "dms.physical.storage.normal",
             "available_zones" : [ "xxx", "xxx" ],
             "volume_type" : "SATA"
           }, {
             "io_type" : "high",
             "storage_spec_code" : "dms.physical.storage.high",
             "unavailable_zones" : [ "xxx", "xxx" ],
             "available_zones" : [ ],
             "volume_type" : "SAS"
           }, {
             "io_type" : "ultra",
             "storage_spec_code" : "dms.physical.storage.ultra",
             "unavailable_zones" : [ "xxx", "xxx" ],
             "available_zones" : [ ],
             "volume_type" : "SSD"
           } ],
           "bandwidth" : "100MB",
           "unavailable_zones" : [ "xxx", "xxx" ],
           "available_zones" : [ "xxx" ],
           "ecs_flavor_id" : "s6.large.2",
           "arch_type" : "X86"
         }, {
           "tps" : "100000",
           "storage_space" : "1200",
           "partition_num" : "900",
           "product_id" : "00300-30310-0--0",
           "spec_code" : "dms.instance.kafka.cluster.c3.small.2",
           "io" : [ {
             "io_type" : "normal",
             "storage_spec_code" : "dms.physical.storage.normal",
             "available_zones" : [ "xxx", "xxx" ],
             "volume_type" : "SATA"
           }, {
             "io_type" : "high",
             "storage_spec_code" : "dms.physical.storage.high",
             "unavailable_zones" : [ "xxx", "xxx" ],
             "available_zones" : [ ],
             "volume_type" : "SAS"
           }, {
             "io_type" : "ultra",
             "storage_spec_code" : "dms.physical.storage.ultra",
             "unavailable_zones" : [ "xxx", "xxx" ],
             "available_zones" : [ ],
             "volume_type" : "SSD"
           } ],
           "bandwidth" : "300MB",
           "unavailable_zones" : [ "xxx", "xxx" ],
           "available_zones" : [ "xxx" ],
           "ecs_flavor_id" : "c3.medium.2",
           "arch_type" : "X86"
         } ],
         "name" : "cluster",
         "unavailable_zones" : [ "xxx", "xxx" ],
         "available_zones" : [ "xxx" ]
       } ]
     } ],
     "Monthly" : [ {
       "name" : "kafka",
       "version" : "1.1.0",
       "values" : [ {
         "detail" : [ {
           "tps" : "50000",
           "storage_space" : "200",
           "partition_num" : "300",
           "product_id" : "00300-30309-0--0",
           "spec_code" : "dms.instance.kafka.cluster.c3.mini",
           "io" : [ {
             "io_type" : "normal",
             "storage_spec_code" : "dms.physical.storage.normal",
             "available_zones" : [ "xxx", "xxx" ],
             "volume_type" : "SATA"
           }, {
             "io_type" : "high",
             "storage_spec_code" : "dms.physical.storage.high",
             "unavailable_zones" : [ "xxx", "xxx" ],
             "available_zones" : [ ],
             "volume_type" : "SAS"
           }, {
             "io_type" : "ultra",
             "storage_spec_code" : "dms.physical.storage.ultra",
             "unavailable_zones" : [ "xxx", "xxx" ],
             "available_zones" : [ ],
             "volume_type" : "SSD"
           } ],
           "bandwidth" : "100MB",
           "unavailable_zones" : [ "xxx", "xxx" ],
           "available_zones" : [ "xxx" ],
           "ecs_flavor_id" : "s6.large.2",
           "arch_type" : "X86"
         }, {
           "tps" : "100000",
           "storage_space" : "1200",
           "partition_num" : "900",
           "product_id" : "00300-30311-0--0",
           "spec_code" : "dms.instance.kafka.cluster.c3.small.2",
           "io" : [ {
             "io_type" : "normal",
             "storage_spec_code" : "dms.physical.storage.normal",
             "available_zones" : [ "xxx", "xxx" ],
             "volume_type" : "SATA"
           }, {
             "io_type" : "high",
             "storage_spec_code" : "dms.physical.storage.high",
             "unavailable_zones" : [ "xxx", "xxx" ],
             "available_zones" : [ ],
             "volume_type" : "SAS"
           }, {
             "io_type" : "ultra",
             "storage_spec_code" : "dms.physical.storage.ultra",
             "unavailable_zones" : [ "xxx", "xxx" ],
             "available_zones" : [ ],
             "volume_type" : "SSD"
           } ],
           "bandwidth" : "300MB",
           "unavailable_zones" : [ "xxx", "xxx" ],
           "available_zones" : [ "xxx" ],
           "ecs_flavor_id" : "c3.medium.2",
           "arch_type" : "X86"
         } ],
         "name" : "cluster",
         "unavailable_zones" : [ "xxx", "xxx" ],
         "available_zones" : [ "xxx" ]
       } ]
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
