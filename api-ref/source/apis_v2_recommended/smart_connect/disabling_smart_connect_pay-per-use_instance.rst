:original_name: DeleteConnector.html

.. _DeleteConnector:

Disabling Smart Connect (Pay-per-Use Instance)
==============================================

Function
--------

This API is used to disable Smart Connect for a pay-per-use instance.

URI
---

POST /v2/{project_id}/kafka/instances/{instance_id}/delete-connector

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

   +-----------+--------+---------------------------------------------------------------+
   | Parameter | Type   | Description                                                   |
   +===========+========+===============================================================+
   | job_id    | String | ID of the job for asynchronously executing the deletion task. |
   +-----------+--------+---------------------------------------------------------------+

Example Requests
----------------

.. code-block:: text

   POST https://{endpoint}/v2/{project_id}/kafka/instances/{instance_id}/delete-connector

Example Responses
-----------------

**Status code: 200**

Smart Connect disabling task submitted successfully.

.. code-block::

   {
     "job_id" : "d366178c-29ea-4d5c-a344-fa2ece4a1836"
   }

Status Codes
------------

=========== ====================================================
Status Code Description
=========== ====================================================
200         Smart Connect disabling task submitted successfully.
=========== ====================================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
