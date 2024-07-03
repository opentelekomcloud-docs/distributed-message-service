:original_name: UpdateInstanceCrossVpcIp.html

.. _UpdateInstanceCrossVpcIp:

Modifying the Private IP Address for Cross-VPC Access
=====================================================

Function
--------

This API is used to modify the private IP address for cross-VPC access.

URI
---

POST /v2/{project_id}/instances/{instance_id}/crossvpc/modify

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

   +------------------------+-----------------+--------------------+----------------------------------------------------------------------+
   | Parameter              | Mandatory       | Type               | Description                                                          |
   +========================+=================+====================+======================================================================+
   | advertised_ip_contents | Yes             | Map<String,String> | User-defined advertised_ip_contents key-value pair.                  |
   |                        |                 |                    |                                                                      |
   |                        |                 |                    | The key is the listeners IP address.                                 |
   |                        |                 |                    |                                                                      |
   |                        |                 |                    | The value is the advertised.listeners IP address or domain name.     |
   |                        |                 |                    |                                                                      |
   |                        |                 |                    | .. note::                                                            |
   |                        |                 |                    |                                                                      |
   |                        |                 |                    |    Fill in the items that are not modified during IP address change. |
   +------------------------+-----------------+--------------------+----------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-----------+------------------------------------------------------------------------------+-------------------------------------------------------------+
   | Parameter | Type                                                                         | Description                                                 |
   +===========+==============================================================================+=============================================================+
   | success   | Boolean                                                                      | Result of the cross-VPC access modification.                |
   +-----------+------------------------------------------------------------------------------+-------------------------------------------------------------+
   | results   | Array of :ref:`results <updateinstancecrossvpcip__response_results>` objects | Details of the result of the cross-VPC access modification. |
   +-----------+------------------------------------------------------------------------------+-------------------------------------------------------------+

.. _updateinstancecrossvpcip__response_results:

.. table:: **Table 4** results

   ============= ======= ===============================================
   Parameter     Type    Description
   ============= ======= ===============================================
   advertised_ip String  advertised.listeners IP address or domain name.
   success       Boolean Status of the cross-VPC access modification.
   ip            String  Listeners IP address.
   ============= ======= ===============================================

Example Requests
----------------

Modifying the private IP address for cross-VPC access.

.. code-block:: text

   POST https://{endpoint}/v2/{project_id}/instances/{instance_id}/crossvpc/modify

   {
     "advertised_ip_contents" : {
       "192.168.245.246" : "192.168.245.247",
       "192.168.197.36" : "192.168.197.38",
       "192.168.190.11" : "192.168.190.11"
     }
   }

Example Responses
-----------------

**Status code: 200**

The private IP address for cross-VPC access is modified successfully.

.. code-block::

   {
     "success" : true,
     "results" : [ {
       "advertised_ip" : "192.168.197.36",
       "success" : true,
       "ip" : "192.168.197.36"
     }, {
       "advertised_ip" : "192.168.190.11",
       "success" : true,
       "ip" : "192.168.190.11"
     }, {
       "advertised_ip" : "192.168.245.255",
       "success" : true,
       "ip" : "192.168.245.246"
     } ]
   }

Status Codes
------------

+-------------+-----------------------------------------------------------------------+
| Status Code | Description                                                           |
+=============+=======================================================================+
| 200         | The private IP address for cross-VPC access is modified successfully. |
+-------------+-----------------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
