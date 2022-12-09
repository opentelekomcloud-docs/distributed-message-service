:original_name: ShowMaintainWindows.html

.. _ShowMaintainWindows:

Listing Maintenance Time Windows
================================

Function
--------

This API is used to query the start time and end time of maintenance time windows.

URI
---

GET /v2/instances/maintain-windows

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 1** Response body parameters

   +------------------+-----------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Parameter        | Type                                                                                                | Description                                 |
   +==================+=====================================================================================================+=============================================+
   | maintain_windows | Array of :ref:`MaintainWindowsEntity <showmaintainwindows__response_maintainwindowsentity>` objects | List of supported maintenance time windows. |
   +------------------+-----------------------------------------------------------------------------------------------------+---------------------------------------------+

.. _showmaintainwindows__response_maintainwindowsentity:

.. table:: **Table 2** MaintainWindowsEntity

   +-----------+---------+-------------------------------------------------------------------------+
   | Parameter | Type    | Description                                                             |
   +===========+=========+=========================================================================+
   | default   | Boolean | Whether the maintenance time window is set to the default time segment. |
   +-----------+---------+-------------------------------------------------------------------------+
   | end       | String  | End time of the maintenance time window.                                |
   +-----------+---------+-------------------------------------------------------------------------+
   | begin     | String  | Start time of the maintenance time window.                              |
   +-----------+---------+-------------------------------------------------------------------------+
   | seq       | Integer | Sequence number.                                                        |
   +-----------+---------+-------------------------------------------------------------------------+

Example Requests
----------------

.. code-block:: text

   GET https://{endpoint}/v2/instances/maintain-windows

Example Responses
-----------------

**Status code: 200**

The consumption of the message is successfully acknowledged.

.. code-block::

   {
     "maintain_windows" : [ {
       "default" : false,
       "seq" : 1,
       "begin" : "22",
       "end" : "02"
     }, {
       "default" : true,
       "seq" : 2,
       "begin" : "02",
       "end" : "06"
     }, {
       "default" : false,
       "seq" : 3,
       "begin" : "06",
       "end" : "10"
     }, {
       "default" : false,
       "seq" : 4,
       "begin" : "10",
       "end" : "14"
     }, {
       "default" : false,
       "seq" : 5,
       "begin" : "14",
       "end" : "18"
     }, {
       "default" : false,
       "seq" : 6,
       "begin" : "18",
       "end" : "22"
     } ]
   }

Status Codes
------------

=========== ============================================================
Status Code Description
=========== ============================================================
200         The consumption of the message is successfully acknowledged.
=========== ============================================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
