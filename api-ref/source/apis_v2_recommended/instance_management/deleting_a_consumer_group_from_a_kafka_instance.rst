:original_name: DeleteGroup.html

.. _DeleteGroup:

Deleting a Consumer Group from a Kafka Instance
===============================================

Function
--------

This API is used to delete a consumer group from a Kafka instance.

URI
---

DELETE /v2/{project_id}/instances/{instance_id}/groups/{group}

.. table:: **Table 1** Path Parameters

   =========== ========= ====== ==================
   Parameter   Mandatory Type   Description
   =========== ========= ====== ==================
   project_id  Yes       String Project ID.
   instance_id Yes       String Instance ID.
   group       Yes       String Consumer group ID.
   =========== ========= ====== ==================

Request Parameters
------------------

None

Response Parameters
-------------------

None

Example Requests
----------------

.. code-block:: text

   DELETE https://{endpoint}/v2/{project_id}/instances/{instance_id}/groups/{group}

Example Responses
-----------------

None

Status Codes
------------

=========== ===========================
Status Code Description
=========== ===========================
204         The deletion is successful.
=========== ===========================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
