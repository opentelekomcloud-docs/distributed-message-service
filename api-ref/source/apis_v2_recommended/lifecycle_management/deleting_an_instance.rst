:original_name: DeleteInstance.html

.. _DeleteInstance:

Deleting an Instance
====================

Function
--------

This API is used to delete an instance to release all the resources occupied by it.

URI
---

DELETE /v2/{project_id}/instances/{instance_id}

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

None

Example Requests
----------------

.. code-block:: text

   DELETE https://{endpoint}/v2/{project_id}/instances/{instance_id}

Example Responses
-----------------

None

Status Codes
------------

=========== ===============================================
Status Code Description
=========== ===============================================
204         The specified instance is deleted successfully.
=========== ===============================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
