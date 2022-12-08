:original_name: ShowInstanceUsers.html

.. _ShowInstanceUsers:

Querying the User List
======================

Function
--------

This API is used to query the user list.

User management is supported only when SASL is enabled for the Kafka instance.

URI
---

GET /v2/{project_id}/instances/{instance_id}/users

.. table:: **Table 1** Path Parameters

   =========== ========= ====== ============
   Parameter   Mandatory Type   Description
   =========== ========= ====== ============
   project_id  Yes       String Project ID.
   instance_id Yes       String Instance ID.
   =========== ========= ====== ============

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameters

   +-----------+-------------------------------------------------------------------------------------------------------+-------------+
   | Parameter | Type                                                                                                  | Description |
   +===========+=======================================================================================================+=============+
   | users     | Array of :ref:`ShowInstanceUsersEntity <showinstanceusers__response_showinstanceusersentity>` objects | User list.  |
   +-----------+-------------------------------------------------------------------------------------------------------+-------------+

.. _showinstanceusers__response_showinstanceusersentity:

.. table:: **Table 3** ShowInstanceUsersEntity

   ============ ======= ==================================================
   Parameter    Type    Description
   ============ ======= ==================================================
   user_name    String  Username.
   role         String  User role.
   default_app  Boolean Whether an application is the default application.
   created_time Long    Creation time.
   ============ ======= ==================================================

Example Requests
----------------

Querying the user list.

.. code-block:: text

   GET https://{endpoint}/v2/{project_id}/instances/{instance_id}/users

Example Responses
-----------------

**Status code: 200**

The query is successful.

.. code-block::

   {
     "users" : [ {
       "user_name" : "xxxa",
       "role" : "guest",
       "default_app" : false,
       "created_time" : 1615431764734
     }, {
       "user_name" : "test",
       "role" : "guest",
       "default_app" : false,
       "created_time" : 1615364062463
     }, {
       "user_name" : "ROOT",
       "role" : "guest",
       "default_app" : false,
       "created_time" : 1617194246328
     } ]
   }

Status Codes
------------

=========== ========================
Status Code Description
=========== ========================
200         The query is successful.
=========== ========================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
