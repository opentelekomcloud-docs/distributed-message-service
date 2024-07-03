:original_name: UpdateInstanceAutoCreateTopic.html

.. _UpdateInstanceAutoCreateTopic:

Configuring Automatic Topic Creation
====================================

Function
--------

This API is used to enable or disable automatic topic creation.

URI
---

POST /v2/{project_id}/instances/{instance_id}/autotopic

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

   +-------------------+-----------+---------+---------------------------------------------+
   | Parameter         | Mandatory | Type    | Description                                 |
   +===================+===========+=========+=============================================+
   | enable_auto_topic | Yes       | Boolean | Whether to enable automatic topic creation. |
   +-------------------+-----------+---------+---------------------------------------------+

Response Parameters
-------------------

None

Example Requests
----------------

Enabling automatic topic creation.

.. code-block:: text

   POST https://{endpoint}/v2/{project_id}/instances/{instance_id}/autotopic

   {
     "enable_auto_topic" : true
   }

Example Responses
-----------------

None

Status Codes
------------

=========== =================================================
Status Code Description
=========== =================================================
200         The function is enabled or disabled successfully.
=========== =================================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
