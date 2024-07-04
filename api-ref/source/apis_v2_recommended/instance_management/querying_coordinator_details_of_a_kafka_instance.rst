:original_name: ShowCoordinators.html

.. _ShowCoordinators:

Querying Coordinator Details of a Kafka Instance
================================================

Function
--------

This API is used to query coordinator details of a Kafka instance.

URI
---

GET /v2/{project_id}/instances/{instance_id}/management/coordinators

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

   +--------------+--------------------------------------------------------------------------------+----------------------------------------------+
   | Parameter    | Type                                                                           | Description                                  |
   +==============+================================================================================+==============================================+
   | coordinators | Array of :ref:`coordinators <showcoordinators__response_coordinators>` objects | List of coordinators of all consumer groups. |
   +--------------+--------------------------------------------------------------------------------+----------------------------------------------+

.. _showcoordinators__response_coordinators:

.. table:: **Table 3** coordinators

   ========= ======= =============================
   Parameter Type    Description
   ========= ======= =============================
   group_id  String  Consumer group ID.
   id        Integer Broker ID of the coordinator.
   host      String  Address of the coordinator.
   port      Integer Port number.
   ========= ======= =============================

Example Requests
----------------

.. code-block:: text

   GET https://{endpoint}/v2/{project_id}/instances/{instance_id}/management/coordinators

Example Responses
-----------------

**Status code: 200**

Coordinator details of the Kafka instance are queried successfully.

.. code-block::

   {
     "coordinators" : [ {
       "group_id" : "XXXX",
       "id" : 2,
       "host" : "172.31.1.15",
       "port" : 9091
     }, {
       "group_id" : "XXXX",
       "id" : 2,
       "host" : "172.31.1.15",
       "port" : 9092
     }, {
       "group_id" : "XXXX",
       "id" : 2,
       "host" : "172.31.1.15",
       "port" : 9092
     } ]
   }

Status Codes
------------

+-------------+---------------------------------------------------------------------+
| Status Code | Description                                                         |
+=============+=====================================================================+
| 200         | Coordinator details of the Kafka instance are queried successfully. |
+-------------+---------------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
