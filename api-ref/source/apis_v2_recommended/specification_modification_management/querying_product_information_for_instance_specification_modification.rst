:original_name: ShowInstanceExtendProductInfo.html

.. _ShowInstanceExtendProductInfo:

Querying Product Information for Instance Specification Modification
====================================================================

Function
--------

This API is used to query the product information for instance specification modification.

URI
---

GET /v2/{project_id}/instances/{instance_id}/extend

.. table:: **Table 1** Path Parameters

   =========== ========= ====== ============
   Parameter   Mandatory Type   Description
   =========== ========= ====== ============
   project_id  Yes       String Project ID.
   instance_id Yes       String Instance ID.
   =========== ========= ====== ============

.. table:: **Table 2** Query Parameters

   +-----------------+-----------------+-----------------+-------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                     |
   +=================+=================+=================+=================================================+
   | type            | Yes             | String          | -  **platinum**: platinum edition               |
   +-----------------+-----------------+-----------------+-------------------------------------------------+
   | engine          | Yes             | String          | Message engine. Currently supported: **kafka**. |
   +-----------------+-----------------+-----------------+-------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-----------+-----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Type                                                                              | Description                                                                                                                   |
   +===========+===================================================================================+===============================================================================================================================+
   | hourly    | Array of :ref:`hourly <showinstanceextendproductinfo__response_hourly>` objects   | List of products.                                                                                                             |
   +-----------+-----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
   | monthly   | Array of :ref:`monthly <showinstanceextendproductinfo__response_monthly>` objects | List of products in yearly/monthly billing mode. Currently, you cannot create yearly/monthly Kafka instances by calling APIs. |
   +-----------+-----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+

.. _showinstanceextendproductinfo__response_hourly:

.. table:: **Table 4** hourly

   +-----------+---------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | Parameter | Type                                                                            | Description                                                                  |
   +===========+=================================================================================+==============================================================================+
   | name      | String                                                                          | Message engine, which is **kafka**.                                          |
   +-----------+---------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | version   | String                                                                          | Version of the message engine. Currently, only 1.1.0 and 2.3.0 is supported. |
   +-----------+---------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | values    | Array of :ref:`values <showinstanceextendproductinfo__response_values>` objects | Product specifications.                                                      |
   +-----------+---------------------------------------------------------------------------------+------------------------------------------------------------------------------+

.. _showinstanceextendproductinfo__response_values:

.. table:: **Table 5** values

   +-------------------+---------------------------------------------------------------------------------+--------------------------------------------------+
   | Parameter         | Type                                                                            | Description                                      |
   +===================+=================================================================================+==================================================+
   | detail            | Array of :ref:`detail <showinstanceextendproductinfo__response_detail>` objects | Specification details.                           |
   +-------------------+---------------------------------------------------------------------------------+--------------------------------------------------+
   | name              | String                                                                          | Instance type.                                   |
   +-------------------+---------------------------------------------------------------------------------+--------------------------------------------------+
   | unavailable_zones | Array of strings                                                                | AZs where resources are sold out.                |
   +-------------------+---------------------------------------------------------------------------------+--------------------------------------------------+
   | available_zones   | Array of strings                                                                | List of AZs where there are available resources. |
   +-------------------+---------------------------------------------------------------------------------+--------------------------------------------------+

.. _showinstanceextendproductinfo__response_detail:

.. table:: **Table 6** detail

   +--------------------------+-------------------------------------------------------------------------+--------------------------------------------------------------------+
   | Parameter                | Type                                                                    | Description                                                        |
   +==========================+=========================================================================+====================================================================+
   | tps                      | String                                                                  | Maximum number of messages per unit time.                          |
   +--------------------------+-------------------------------------------------------------------------+--------------------------------------------------------------------+
   | storage                  | String                                                                  | Message storage space.                                             |
   +--------------------------+-------------------------------------------------------------------------+--------------------------------------------------------------------+
   | partition_num            | String                                                                  | Number of partitions in a Kafka instance.                          |
   +--------------------------+-------------------------------------------------------------------------+--------------------------------------------------------------------+
   | product_id               | String                                                                  | Product ID.                                                        |
   +--------------------------+-------------------------------------------------------------------------+--------------------------------------------------------------------+
   | spec_code                | String                                                                  | Specification ID.                                                  |
   +--------------------------+-------------------------------------------------------------------------+--------------------------------------------------------------------+
   | io                       | Array of :ref:`io <showinstanceextendproductinfo__response_io>` objects | I/O information.                                                   |
   +--------------------------+-------------------------------------------------------------------------+--------------------------------------------------------------------+
   | bandwidth                | String                                                                  | Bandwidth of a Kafka instance.                                     |
   +--------------------------+-------------------------------------------------------------------------+--------------------------------------------------------------------+
   | recommend_max_consGroups | String                                                                  | Recommended maximum number of consumer groups of a Kafka instance. |
   +--------------------------+-------------------------------------------------------------------------+--------------------------------------------------------------------+
   | unavailable_zones        | Array of strings                                                        | AZs where resources are sold out.                                  |
   +--------------------------+-------------------------------------------------------------------------+--------------------------------------------------------------------+
   | available_zones          | Array of strings                                                        | List of AZs where there are available resources.                   |
   +--------------------------+-------------------------------------------------------------------------+--------------------------------------------------------------------+
   | ecs_flavor_id            | String                                                                  | Flavor of the corresponding ECS.                                   |
   +--------------------------+-------------------------------------------------------------------------+--------------------------------------------------------------------+
   | arch_type                | String                                                                  | Instance architecture type. Currently, only x86 is supported.      |
   +--------------------------+-------------------------------------------------------------------------+--------------------------------------------------------------------+

.. _showinstanceextendproductinfo__response_io:

.. table:: **Table 7** io

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

.. _showinstanceextendproductinfo__response_monthly:

.. table:: **Table 8** monthly

   +-----------+-----------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | Parameter | Type                                                                              | Description                                                                  |
   +===========+===================================================================================+==============================================================================+
   | name      | String                                                                            | Message engine, which is **kafka**.                                          |
   +-----------+-----------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | version   | String                                                                            | Version of the message engine. Currently, only 1.1.0 and 2.3.0 is supported. |
   +-----------+-----------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | values    | Array of :ref:`values <showinstanceextendproductinfo__response_values_1>` objects | Product specifications.                                                      |
   +-----------+-----------------------------------------------------------------------------------+------------------------------------------------------------------------------+

.. _showinstanceextendproductinfo__response_values_1:

.. table:: **Table 9** values

   +-------------------+-----------------------------------------------------------------------------------+--------------------------------------------------+
   | Parameter         | Type                                                                              | Description                                      |
   +===================+===================================================================================+==================================================+
   | detail            | Array of :ref:`detail <showinstanceextendproductinfo__response_detail_1>` objects | Specification details.                           |
   +-------------------+-----------------------------------------------------------------------------------+--------------------------------------------------+
   | name              | String                                                                            | Instance type.                                   |
   +-------------------+-----------------------------------------------------------------------------------+--------------------------------------------------+
   | unavailable_zones | Array of strings                                                                  | AZs where resources are sold out.                |
   +-------------------+-----------------------------------------------------------------------------------+--------------------------------------------------+
   | available_zones   | Array of strings                                                                  | List of AZs where there are available resources. |
   +-------------------+-----------------------------------------------------------------------------------+--------------------------------------------------+

.. _showinstanceextendproductinfo__response_detail_1:

.. table:: **Table 10** detail

   +-------------------+---------------------------------------------------------------------------+---------------------------------------------------------------+
   | Parameter         | Type                                                                      | Description                                                   |
   +===================+===========================================================================+===============================================================+
   | tps               | String                                                                    | Maximum number of messages per unit time.                     |
   +-------------------+---------------------------------------------------------------------------+---------------------------------------------------------------+
   | storage           | String                                                                    | Message storage space.                                        |
   +-------------------+---------------------------------------------------------------------------+---------------------------------------------------------------+
   | partition_num     | String                                                                    | Number of partitions in a Kafka instance.                     |
   +-------------------+---------------------------------------------------------------------------+---------------------------------------------------------------+
   | product_id        | String                                                                    | Product ID.                                                   |
   +-------------------+---------------------------------------------------------------------------+---------------------------------------------------------------+
   | spec_code         | String                                                                    | Specification ID.                                             |
   +-------------------+---------------------------------------------------------------------------+---------------------------------------------------------------+
   | io                | Array of :ref:`io <showinstanceextendproductinfo__response_io_1>` objects | I/O information.                                              |
   +-------------------+---------------------------------------------------------------------------+---------------------------------------------------------------+
   | bandwidth         | String                                                                    | Bandwidth of a Kafka instance.                                |
   +-------------------+---------------------------------------------------------------------------+---------------------------------------------------------------+
   | unavailable_zones | Array of strings                                                          | AZs where resources are sold out.                             |
   +-------------------+---------------------------------------------------------------------------+---------------------------------------------------------------+
   | available_zones   | Array of strings                                                          | List of AZs where there are available resources.              |
   +-------------------+---------------------------------------------------------------------------+---------------------------------------------------------------+
   | ecs_flavor_id     | String                                                                    | Flavor of the corresponding ECS.                              |
   +-------------------+---------------------------------------------------------------------------+---------------------------------------------------------------+
   | arch_type         | String                                                                    | Instance architecture type. Currently, only x86 is supported. |
   +-------------------+---------------------------------------------------------------------------+---------------------------------------------------------------+

.. _showinstanceextendproductinfo__response_io_1:

.. table:: **Table 11** io

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

   GET https://{endpoint}/v2/{project_id}/instances/{instance_id}/extend?type={type}&engine={engine}

Example Responses
-----------------

**Status code: 200**

The query is successful.

.. code-block::

   {
     "hourly" : [ {
       "name" : "kafka",
       "version" : "1.1.0",
       "values" : [ {
         "detail" : [ {
           "tps" : "50000",
           "storage" : "200",
           "partition_num" : "300",
           "product_id" : "00300-30316-0--0",
           "spec_code" : "kafka.c3.mini.connector",
           "io" : [ {
             "io_type" : "high",
             "storage_spec_code" : "dms.physical.storage.high",
             "available_zones" : [ "xxx", "xxx" ],
             "volume_type" : "SAS"
           }, {
             "io_type" : "ultra",
             "storage_spec_code" : "dms.physical.storage.ultra",
             "available_zones" : [ "xxx", "xxx" ],
             "volume_type" : "SSD"
           } ],
           "bandwidth" : "100MB",
           "recommend_max_consGroups" : "60",
           "unavailable_zones" : [ "xxx", "xxx" ],
           "available_zones" : [ "xxx", "xxx" ],
           "ecs_flavor_id" : "c6.large.2",
           "arch_type" : "X86"
         }, {
           "tps" : "100000",
           "storage" : "396",
           "partition_num" : "900",
           "product_id" : "00300-30340-0--0",
           "spec_code" : "kafka.c3.small.2.connector",
           "io" : [ {
             "io_type" : "high",
             "storage_spec_code" : "dms.physical.storage.high",
             "available_zones" : [ "xxx", "xxx" ],
             "volume_type" : "SAS"
           }, {
             "io_type" : "ultra",
             "storage_spec_code" : "dms.physical.storage.ultra",
             "available_zones" : [ "xxx", "xxx" ],
             "volume_type" : "SSD"
           } ],
           "bandwidth" : "300MB",
           "recommend_max_consGroups" : "300",
           "unavailable_zones" : [ "xxx", "xxx" ],
           "available_zones" : [ "xxx", "xxx" ],
           "ecs_flavor_id" : "c6.xlarge.2",
           "arch_type" : "X86"
         }, {
           "tps" : "200000",
           "storage" : "1056",
           "partition_num" : "1800",
           "product_id" : "00300-30342-0--0",
           "spec_code" : "kafka.c3.middle.2.connector",
           "io" : [ {
             "io_type" : "high",
             "storage_spec_code" : "dms.physical.storage.high",
             "available_zones" : [ "xxx", "xxx" ],
             "volume_type" : "SAS"
           }, {
             "io_type" : "ultra",
             "storage_spec_code" : "dms.physical.storage.ultra",
             "available_zones" : [ "xxx", "xxx" ],
             "volume_type" : "SSD"
           } ],
           "bandwidth" : "600MB",
           "recommend_max_consGroups" : "600",
           "unavailable_zones" : [ "xxx", "xxx" ],
           "available_zones" : [ "xxx", "xxx" ],
           "ecs_flavor_id" : "c6.2xlarge.2",
           "arch_type" : "X86"
         }, {
           "tps" : "300000",
           "storage" : "2112",
           "partition_num" : "1800",
           "product_id" : "00300-30344-0--0",
           "spec_code" : "kafka.c3.high.2.connector",
           "io" : [ {
             "io_type" : "high",
             "storage_spec_code" : "dms.physical.storage.high",
             "available_zones" : [ "xxx", "xxx" ],
             "volume_type" : "SAS"
           }, {
             "io_type" : "ultra",
             "storage_spec_code" : "dms.physical.storage.ultra",
             "available_zones" : [ "xxx", "xxx" ],
             "volume_type" : "SSD"
           } ],
           "bandwidth" : "1200MB",
           "recommend_max_consGroups" : "600",
           "unavailable_zones" : [ "xxx", "xxx" ],
           "available_zones" : [ "xxx", "xxx" ],
           "ecs_flavor_id" : "c6.2xlarge.2",
           "arch_type" : "X86"
         } ],
         "name" : "cluster",
         "unavailable_zones" : [ "xxx", "xxx" ],
         "available_zones" : [ "xxx", "xxx" ]
       } ]
     } ],
     "monthly" : [ {
       "name" : "kafka",
       "version" : "1.1.0",
       "values" : [ {
         "detail" : [ {
           "tps" : "50000",
           "storage" : "200",
           "partition_num" : "300",
           "product_id" : "00300-30317-0--0",
           "spec_code" : "kafka.c3.mini.connector",
           "io" : [ {
             "io_type" : "high",
             "storage_spec_code" : "dms.physical.storage.high",
             "available_zones" : [ "xxx", "xxx" ],
             "volume_type" : "SAS"
           }, {
             "io_type" : "ultra",
             "storage_spec_code" : "dms.physical.storage.ultra",
             "available_zones" : [ "xxx", "xxx" ],
             "volume_type" : "SSD"
           } ],
           "bandwidth" : "100MB",
           "recommend_max_consGroups" : "60",
           "unavailable_zones" : [ "xxx", "xxx" ],
           "available_zones" : [ "xxx", "xxx" ],
           "ecs_flavor_id" : "c6.large.2",
           "arch_type" : "X86"
         }, {
           "tps" : "100000",
           "storage" : "396",
           "partition_num" : "900",
           "product_id" : "00300-30341-0--0",
           "spec_code" : "kafka.c3.small.2.connector",
           "io" : [ {
             "io_type" : "high",
             "storage_spec_code" : "dms.physical.storage.high",
             "available_zones" : [ "xxx", "xxx" ],
             "volume_type" : "SAS"
           }, {
             "io_type" : "ultra",
             "storage_spec_code" : "dms.physical.storage.ultra",
             "available_zones" : [ "xxx", "xxx" ],
             "volume_type" : "SSD"
           } ],
           "bandwidth" : "300MB",
           "recommend_max_consGroups" : "300",
           "unavailable_zones" : [ "xxx", "xxx" ],
           "available_zones" : [ "xxx", "xxx" ],
           "ecs_flavor_id" : "c6.xlarge.2",
           "arch_type" : "X86"
         }, {
           "tps" : "200000",
           "storage" : "1056",
           "partition_num" : "1800",
           "product_id" : "00300-30343-0--0",
           "spec_code" : "kafka.c3.middle.2.connector",
           "io" : [ {
             "io_type" : "high",
             "storage_spec_code" : "dms.physical.storage.high",
             "available_zones" : [ "xxx", "xxx" ],
             "volume_type" : "SAS"
           }, {
             "io_type" : "ultra",
             "storage_spec_code" : "dms.physical.storage.ultra",
             "available_zones" : [ "xxx", "xxx" ],
             "volume_type" : "SSD"
           } ],
           "bandwidth" : "600MB",
           "recommend_max_consGroups" : "600",
           "unavailable_zones" : [ "xxx", "xxx" ],
           "available_zones" : [ "xxx", "xxx" ],
           "ecs_flavor_id" : "c6.2xlarge.2",
           "arch_type" : "X86"
         }, {
           "tps" : "300000",
           "storage" : "2112",
           "partition_num" : "1800",
           "product_id" : "00300-30345-0--0",
           "spec_code" : "kafka.c3.high.2.connector",
           "io" : [ {
             "io_type" : "high",
             "storage_spec_code" : "dms.physical.storage.high",
             "available_zones" : [ "xxx", "xxx" ],
             "volume_type" : "SAS"
           }, {
             "io_type" : "ultra",
             "storage_spec_code" : "dms.physical.storage.ultra",
             "available_zones" : [ "xxx", "xxx" ],
             "volume_type" : "SSD"
           } ],
           "bandwidth" : "1200MB",
           "recommend_max_consGroups" : "600",
           "unavailable_zones" : [ "xxx", "xxx" ],
           "available_zones" : [ "xxx", "xxx" ],
           "ecs_flavor_id" : "c6.2xlarge.2",
           "arch_type" : "X86"
         } ],
         "name" : "cluster",
         "unavailable_zones" : [ "xxx", "xxx" ],
         "available_zones" : [ "xxx", "xxx" ]
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
