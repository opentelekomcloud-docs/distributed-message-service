:original_name: ResizeEngineInstance.html

.. _ResizeEngineInstance:

Increasing Instance Specifications
==================================

Function
--------

This API is used to modify instance specifications.

URI
---

POST /v2/{engine}/{project_id}/instances/{instance_id}/extend

.. table:: **Table 1** Path Parameters

   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                               |
   +=================+=================+=================+===========================================================================================================+
   | engine          | Yes             | String          | Message engine.                                                                                           |
   |                 |                 |                 |                                                                                                           |
   |                 |                 |                 | Default: **kafka**                                                                                        |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------+
   | project_id      | Yes             | String          | Project ID. For details about how to obtain it, see :ref:`Obtaining a Project ID <kafka-api-0036212547>`. |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------+
   | instance_id     | Yes             | String          | Instance ID.                                                                                              |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   +-------------------------+-----------------+------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter               | Mandatory       | Type             | Description                                                                                                                                                |
   +=========================+=================+==================+============================================================================================================================================================+
   | oper_type               | Yes             | String           | Type of the change.                                                                                                                                        |
   |                         |                 |                  |                                                                                                                                                            |
   |                         |                 |                  | Value:                                                                                                                                                     |
   |                         |                 |                  |                                                                                                                                                            |
   |                         |                 |                  | -  **storage**: Expand the storage space without adding brokers.                                                                                           |
   |                         |                 |                  |                                                                                                                                                            |
   |                         |                 |                  | -  **horizontal**: Add brokers without resizing the storage space of each broker.                                                                          |
   |                         |                 |                  |                                                                                                                                                            |
   |                         |                 |                  | -  **vertical**: Modify the underlying flavor of brokers without adding brokers or storage space.                                                          |
   +-------------------------+-----------------+------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | new_storage_space       | No              | Integer          | New storage space.                                                                                                                                         |
   |                         |                 |                  |                                                                                                                                                            |
   |                         |                 |                  | This parameter is valid and mandatory when **oper_type** is set to **storage** or **horizontal**.                                                          |
   |                         |                 |                  |                                                                                                                                                            |
   |                         |                 |                  | Instance storage space = Number of brokers x Storage space of each broker.                                                                                 |
   |                         |                 |                  |                                                                                                                                                            |
   |                         |                 |                  | If **oper_type** is set to **storage**, the number of brokers remains unchanged, and the storage space of each broker must be expanded by at least 100 GB. |
   |                         |                 |                  |                                                                                                                                                            |
   |                         |                 |                  | If **oper_type** is set to **horizontal**, the storage space of each broker remains unchanged.                                                             |
   +-------------------------+-----------------+------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | new_broker_num          | No              | Integer          | This parameter is valid only when **oper_type** is set to **horizontal**.                                                                                  |
   |                         |                 |                  |                                                                                                                                                            |
   |                         |                 |                  | A maximum of 30 brokers are supported.                                                                                                                     |
   +-------------------------+-----------------+------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | new_product_id          | No              | String           | New product ID for scale-up.                                                                                                                               |
   |                         |                 |                  |                                                                                                                                                            |
   |                         |                 |                  | This parameter is valid and mandatory when **oper_type** is set to **vertical**.                                                                           |
   |                         |                 |                  |                                                                                                                                                            |
   |                         |                 |                  | Obtain the product ID from :ref:`Querying Product Specifications List <listengineproducts>`.                                                               |
   +-------------------------+-----------------+------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | publicip_id             | No              | String           | ID of the EIP bound to the instance.                                                                                                                       |
   |                         |                 |                  |                                                                                                                                                            |
   |                         |                 |                  | Use commas (,) to separate multiple EIP IDs.                                                                                                               |
   |                         |                 |                  |                                                                                                                                                            |
   |                         |                 |                  | This parameter is mandatory when **oper_type** is set to **horizontal**.                                                                                   |
   +-------------------------+-----------------+------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | tenant_ips              | No              | Array of strings | Specified IPv4 private IP addresses.                                                                                                                       |
   |                         |                 |                  |                                                                                                                                                            |
   |                         |                 |                  | The number of specified IP addresses must be less than or equal to the number of new brokers.                                                              |
   |                         |                 |                  |                                                                                                                                                            |
   |                         |                 |                  | If the number of specified IP addresses is less than the number of brokers, the unspecified brokers are randomly assigned private IP addresses.            |
   +-------------------------+-----------------+------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | second_tenant_subnet_id | No              | String           | ID of the standby subnet used by new brokers in instance expansion.                                                                                        |
   |                         |                 |                  |                                                                                                                                                            |
   |                         |                 |                  | This value is transferred when a standby subnet is used in instance expansion.                                                                             |
   |                         |                 |                  |                                                                                                                                                            |
   |                         |                 |                  | Contact customer service to use the value.                                                                                                                 |
   +-------------------------+-----------------+------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   ========= ====== ==========================================
   Parameter Type   Description
   ========= ====== ==========================================
   job_id    String ID of the specification modification task.
   ========= ====== ==========================================

Example Requests
----------------

-  Expanding the storage space (pay-per-use)

   .. code-block:: text

      POST https://{endpoint}/v2/{engine}/{project_id}/instances/{instance_id}/extend

      {
        "oper_type" : "storage",
        "new_storage_space" : 600
      }

-  Adding brokers (pay-per-use)

   .. code-block:: text

      POST https://{endpoint}/v2/{engine}/{project_id}/instances/{instance_id}/extend

      {
        "oper_type" : "horizontal",
        "new_storage_space" : 1600,
        "new_broker_num" : 4,
        "tenant_ips" : [ "127.0.0.1", "127.0.0.2", "127.0.0.3" ]
      }

-  Increasing the broker flavor (pay-per-use)

   .. code-block:: text

      POST https://{endpoint}/v2/{engine}/{project_id}/instances/{instance_id}/extend

      {
        "oper_type" : "vertical",
        "new_product_id" : "c6.4u8g.cluster"
      }

Example Responses
-----------------

**Status code: 200**

Instance specifications increased.

.. code-block::

   {
     "job_id" : "93b94287-728d-4bb1-a158-cb66cb0854e7"
   }

Status Codes
------------

=========== ==================================
Status Code Description
=========== ==================================
200         Instance specifications increased.
=========== ==================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
