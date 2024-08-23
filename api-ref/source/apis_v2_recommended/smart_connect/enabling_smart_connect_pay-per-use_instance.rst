:original_name: CreateConnector.html

.. _CreateConnector:

Enabling Smart Connect (Pay-per-Use Instance)
=============================================

Function
--------

This API is used to enable Smart Connect so you can create a connector.

URI
---

POST /v2/{project_id}/instances/{instance_id}/connector

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

   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                      |
   +=================+=================+=================+==================================================================================================================================================+
   | specification   | No              | String          | Bandwidth for deploying Smart Connect, that is, the maximum amount of data transferred per unit time. Use the bandwidth of the current instance. |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | node_cnt        | No              | String          | Number of connectors. Min.: 2.                                                                                                                   |
   |                 |                 |                 |                                                                                                                                                  |
   |                 |                 |                 | The default value is **2** if it is not specified.                                                                                               |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | spec_code       | No              | String          | Specification code of the connector. This parameter is mandatory only for old instance flavors.                                                  |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   ============ ====== =================
   Parameter    Type   Description
   ============ ====== =================
   job_id       String Task ID.
   connector_id String Instance dump ID.
   ============ ====== =================

Example Requests
----------------

-  To enable Smart Connect for pay-per-use instances using new flavors, set the number of connectors to 2.

   .. code-block:: text

      POST https://{endpoint}/v2/{project_id}/instances/{instance_id}/connector

      {
        "node_cnt" : 2
      }

-  To enable Smart Connect for pay-per-use instances using old flavors, set the size of connectors to 100 MB and the number of them to 2.

   .. code-block:: text

      POST https://{endpoint}/v2/{project_id}/instances/{instance_id}/connector

      {
        "specification" : "100MB",
        "node_cnt" : 2,
        "spec_code" : "kafka.c3.mini.connector"
      }

Example Responses
-----------------

**Status code: 200**

Successful.

.. code-block::

   {
     "job_id" : "7c3ec20c-11de-4df9-acc0-7ef1dea25dfe",
     "connector_id" : "55b78880-9077-4c74-ad5a-6868555f76a4"
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
