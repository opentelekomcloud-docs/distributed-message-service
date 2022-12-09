:original_name: kafka-api-180514005.html

.. _kafka-api-180514005:

Deleting an Instance
====================

.. note::

   This API is out-of-date and may not be maintained in the future. Please use the API described in :ref:`Deleting an Instance <deleteinstance>`.

Function
--------

This API is used to delete an instance to release all the resources occupied by it.

URI
---

DELETE /v1.0/{project_id}/instances/{instance_id}

:ref:`Table 1 <kafka-api-180514005__en-us_topic_0128036935_table3660444102619>` describes the parameters.

.. _kafka-api-180514005__en-us_topic_0128036935_table3660444102619:

.. table:: **Table 1** Parameters

   =========== ====== ========= ==============================
   Parameter   Type   Mandatory Description
   =========== ====== ========= ==============================
   project_id  String Yes       Indicates the ID of a project.
   instance_id String Yes       Indicates the instance ID.
   =========== ====== ========= ==============================

Request
-------

**Request parameters**

None.

**Example request**

.. code-block:: text

   DELETE https://{dms_endpoint}/v1.0/{project_id}/instances/{instance_id}

Response
--------

**Response parameters**

None.

**Example response**

None.

Status Code
-----------

:ref:`Table 2 <kafka-api-180514005__en-us_topic_0128036935_table1467214432612>` describes the status code of successful operations. For details about other status codes, see :ref:`Status Code <kafka-api-0034672261>`.

.. _kafka-api-180514005__en-us_topic_0128036935_table1467214432612:

.. table:: **Table 2** Status code

   =========== =====================================
   Status Code Description
   =========== =====================================
   204         The instance is deleted successfully.
   =========== =====================================
