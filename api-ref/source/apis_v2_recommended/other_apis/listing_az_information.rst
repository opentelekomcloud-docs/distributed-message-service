:original_name: ListAvailableZones.html

.. _ListAvailableZones:

Listing AZ Information
======================

Function
--------

This API is used to query the AZ ID for creating an instance.

URI
---

GET /v2/available-zones

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 1** Response body parameters

   +-----------------+----------------------------------------------------------------------------------------+---------------+
   | Parameter       | Type                                                                                   | Description   |
   +=================+========================================================================================+===============+
   | region_id       | String                                                                                 | Region ID.    |
   +-----------------+----------------------------------------------------------------------------------------+---------------+
   | available_zones | Array of :ref:`available_zones <listavailablezones__response_available_zones>` objects | Array of AZs. |
   +-----------------+----------------------------------------------------------------------------------------+---------------+

.. _listavailablezones__response_available_zones:

.. table:: **Table 2** available_zones

   +-----------------------+---------+--------------------------------------------------+
   | Parameter             | Type    | Description                                      |
   +=======================+=========+==================================================+
   | soldOut               | Boolean | Whether resources are sold out.                  |
   +-----------------------+---------+--------------------------------------------------+
   | id                    | String  | AZ ID.                                           |
   +-----------------------+---------+--------------------------------------------------+
   | code                  | String  | AZ code.                                         |
   +-----------------------+---------+--------------------------------------------------+
   | name                  | String  | AZ name.                                         |
   +-----------------------+---------+--------------------------------------------------+
   | port                  | String  | AZ port.                                         |
   +-----------------------+---------+--------------------------------------------------+
   | resource_availability | String  | Whether there are available resources in the AZ. |
   +-----------------------+---------+--------------------------------------------------+
   | default_az            | Boolean | Whether the AZ is the default AZ.                |
   +-----------------------+---------+--------------------------------------------------+
   | remain_time           | Long    | Remaining time.                                  |
   +-----------------------+---------+--------------------------------------------------+
   | ipv6_enable           | Boolean | Whether IPv6 is supported.                       |
   +-----------------------+---------+--------------------------------------------------+

Example Requests
----------------

.. code-block:: text

   GET https://{endpoint}/v2/available-zones

Example Responses
-----------------

**Status code: 200**

The AZ information is queried successfully.

.. code-block::

   {
     "region_id" : "xxx",
     "available_zones" : [ {
       "soldOut" : false,
       "id" : "d539378ec1314c85b76fefa3f7071458",
       "code" : "xxx",
       "name" : "AZ 2.",
       "port" : "8003",
       "resource_availability" : "true",
       "default_az" : true,
       "remain_time" : 9223372036854776000,
       "ipv6_enable" : false
     }, {
       "soldOut" : false,
       "id" : "9f1c5806706d4c1fb0eb72f0a9b18c77",
       "code" : "xxx",
       "name" : "AZ 3.",
       "port" : "443",
       "resource_availability" : "true",
       "default_az" : false,
       "remain_time" : 9223372036854776000,
       "ipv6_enable" : false
     } ]
   }

Status Codes
------------

=========== ===========================================
Status Code Description
=========== ===========================================
200         The AZ information is queried successfully.
=========== ===========================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
