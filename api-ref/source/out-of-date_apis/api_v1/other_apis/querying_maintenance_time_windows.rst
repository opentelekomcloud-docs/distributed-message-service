:original_name: kafka-api-180514010.html

.. _kafka-api-180514010:

Querying Maintenance Time Windows
=================================

.. note::

   This API is out-of-date and may not be maintained in the future. Please use the API described in :ref:`Listing Maintenance Time Windows <showmaintainwindows>`.

Function
--------

This API is used to query the start and end time of the maintenance window.

URI
---

GET /v1.0/instances/maintain-windows

Request
-------

**Request parameters**

None.

**Example request**

.. code-block:: text

   GET https://{dms_endpoint}/v1.0/instances/maintain-windows

Response
--------

**Response parameters**

:ref:`Table 1 <kafka-api-180514010__en-us_topic_0128036903_table04768576115>` and :ref:`Table 2 <kafka-api-180514010__en-us_topic_0128036903_table748235716115>` describe the response parameters.

.. _kafka-api-180514010__en-us_topic_0128036903_table04768576115:

.. table:: **Table 1** Response parameters

   +------------------+-------+---------------------------------------------------------+
   | Parameter        | Type  | Description                                             |
   +==================+=======+=========================================================+
   | maintain_windows | Array | Indicates a list of supported maintenance time windows. |
   +------------------+-------+---------------------------------------------------------+

.. _kafka-api-180514010__en-us_topic_0128036903_table748235716115:

.. table:: **Table 2** maintain_windows parameter description

   +-----------+---------+---------------------------------------------------------------------------------+
   | Parameter | Type    | Description                                                                     |
   +===========+=========+=================================================================================+
   | seq       | Integer | Indicates the sequential number of a maintenance time window.                   |
   +-----------+---------+---------------------------------------------------------------------------------+
   | begin     | String  | Indicates the time at which a maintenance time window starts.                   |
   +-----------+---------+---------------------------------------------------------------------------------+
   | end       | String  | Indicates the time at which a maintenance time window ends.                     |
   +-----------+---------+---------------------------------------------------------------------------------+
   | default   | Boolean | Indicates whether a maintenance time window is set to the default time segment. |
   +-----------+---------+---------------------------------------------------------------------------------+

**Example response**

.. code-block::

   {
       "maintain_windows": [{
           "default": false,
           "seq": 1,
           "begin": "22:00:00",
           "end": "02:00:00"
       },
       {
           "default": true,
           "seq": 2,
           "begin": "02:00:00",
           "end": "06:00:00"
       },
       {
           "default": false,
           "seq": 3,
           "begin": "06:00:00",
           "end": "10:00:00"
       },
       {
           "default": false,
           "seq": 4,
           "begin": "10:00:00",
           "end": "14:00:00"
       },
       {
           "default": false,
           "seq": 5,
           "begin": "14:00:00",
           "end": "18:00:00"
       },
       {
           "default": false,
           "seq": 6,
           "begin": "18:00:00",
           "end": "22:00:00"
       }]
   }

Status Code
-----------

:ref:`Table 3 <kafka-api-180514010__en-us_topic_0128036903_table155041657181114>` describes the status code of successful operations. For details about other status codes, see :ref:`Status Code <kafka-api-0034672261>`.

.. _kafka-api-180514010__en-us_topic_0128036903_table155041657181114:

.. table:: **Table 3** Status code

   =========== ======================================================
   Status Code Description
   =========== ======================================================
   200         The maintenance time windows are queried successfully.
   =========== ======================================================
