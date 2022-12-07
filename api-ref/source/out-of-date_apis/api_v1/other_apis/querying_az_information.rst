:original_name: kafka-api-180514008.html

.. _kafka-api-180514008:

Querying AZ Information
=======================

.. note::

   This API is out-of-date and may not be maintained in the future. Please use the API described in :ref:`Listing AZ Information <listavailablezones>`.

Function
--------

This API is used to query the AZ ID.

URI
---

GET /v1.0/availableZones

Request
-------

**Request parameters**

None.

**Example request**

.. code-block:: text

   GET https://{dms_endpoint}/v1.0/availableZones

Response
--------

**Response parameters**

:ref:`Table 1 <kafka-api-180514008__en-us_topic_0128036911_table2233942133618>` and :ref:`Table 2 <kafka-api-180514008__en-us_topic_0128036911_table1124311429360>` describe the parameters.

.. _kafka-api-180514008__en-us_topic_0128036911_table2233942133618:

.. table:: **Table 1** Response parameters

   +-----------------+--------+-----------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type   | Description                                                                                                                 |
   +=================+========+=============================================================================================================================+
   | region_id       | String | Indicates the region ID.                                                                                                    |
   +-----------------+--------+-----------------------------------------------------------------------------------------------------------------------------+
   | available_zones | Array  | Indicates details of AZs. For details, see :ref:`Table 2 <kafka-api-180514008__en-us_topic_0128036911_table1124311429360>`. |
   +-----------------+--------+-----------------------------------------------------------------------------------------------------------------------------+

.. _kafka-api-180514008__en-us_topic_0128036911_table1124311429360:

.. table:: **Table 2** available_zones parameter description

   +-----------------------+-----------------------+-------------------------------------------------------+
   | Parameter             | Type                  | Description                                           |
   +=======================+=======================+=======================================================+
   | soldOut               | Boolean               | Indicates whether resources are sold out.             |
   +-----------------------+-----------------------+-------------------------------------------------------+
   | id                    | String                | Indicates the ID of an AZ.                            |
   +-----------------------+-----------------------+-------------------------------------------------------+
   | code                  | String                | Indicates the code of an AZ.                          |
   +-----------------------+-----------------------+-------------------------------------------------------+
   | name                  | String                | Indicates the name of an AZ.                          |
   +-----------------------+-----------------------+-------------------------------------------------------+
   | port                  | String                | Indicates the port number of an AZ.                   |
   +-----------------------+-----------------------+-------------------------------------------------------+
   | resource_availability | String                | Indicates whether an AZ has available resources.      |
   |                       |                       |                                                       |
   |                       |                       | -  **true**: The AZ has available resources.          |
   |                       |                       | -  **false**: Resources of the AZ have been sold out. |
   +-----------------------+-----------------------+-------------------------------------------------------+

**Example response**

.. code-block::

   {
       regionId: "XXXX",
       available_zones:[
          {
               "id":"1d7b939b382c4c3bb3481a8ca10da768",
               "name":"az10.dc1",
               "code":"az10.dc1",
               "port":"8002",
               "resource_availability": "true"
           },
           {
               "id":"1d7b939b382c4c3bb3481a8ca10da769",
               "name":"az10.dc2",
               "code":"az10.dc2",
               "port":"8002",
               "resource_availability": "true"
           }
       ]
   }

Status Code
-----------

:ref:`Table 3 <kafka-api-180514008__en-us_topic_0128036911_table825911423368>` describes the status code of successful operations. For details about other status codes, see :ref:`Status Code <kafka-api-0034672261>`.

.. _kafka-api-180514008__en-us_topic_0128036911_table825911423368:

.. table:: **Table 3** Status code

   =========== ===========================================
   Status Code Description
   =========== ===========================================
   200         The AZ information is successfully queried.
   =========== ===========================================
