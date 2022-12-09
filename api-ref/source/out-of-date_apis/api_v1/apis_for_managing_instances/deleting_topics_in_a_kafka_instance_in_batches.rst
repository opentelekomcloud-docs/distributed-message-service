:original_name: kafka-api-180614003.html

.. _kafka-api-180614003:

Deleting Topics in a Kafka Instance in Batches
==============================================

.. note::

   This API is out-of-date and may not be maintained in the future. Please use the API described in :ref:`Batch Deleting Topics of a Kafka Instance <batchdeleteinstancetopic>`.

Function
--------

This API is used to delete topics in a Kafka instance in batches.

URI
---

POST /v1.0/{project_id}/instances/{instance_id}/topics/delete

:ref:`Table 1 <kafka-api-180614003__en-us_topic_0128036887_table999074314516>` describes the parameter.

.. _kafka-api-180614003__en-us_topic_0128036887_table999074314516:

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

:ref:`Table 2 <kafka-api-180614003__en-us_topic_0128036887_table192144257>` describes the parameter.

.. _kafka-api-180614003__en-us_topic_0128036887_table192144257:

.. table:: **Table 2** Request parameter

   ========= ===== ========= ===========================================
   Parameter Type  Mandatory Description
   ========= ===== ========= ===========================================
   topics    Array Yes       Indicates the list of topics to be deleted.
   ========= ===== ========= ===========================================

**Example request**

.. code-block:: text

   POST https://{dms_endpoint}/v1.0/{project_id}/instances/{instance_id}/topics/delete
   {
     "topics" : ["hah", "aabb"]
    }

Response
--------

**Response parameters**

:ref:`Table 3 <kafka-api-180614003__en-us_topic_0128036887_table10111744455>` describes the parameter.

.. _kafka-api-180614003__en-us_topic_0128036887_table10111744455:

.. table:: **Table 3** Response parameters

   ========= ===== =============================
   Parameter Type  Description
   ========= ===== =============================
   topics    Array Indicates the list of topics.
   ========= ===== =============================

.. table:: **Table 4** topics parameter description

   ========= ======= =========================================
   Parameter Type    Description
   ========= ======= =========================================
   id        String  Indicates the topic name.
   success   Boolean Indicates whether the topics are deleted.
   ========= ======= =========================================

**Example response**

.. code-block::

   {
     "topics" : [{
         "id" : "haha",
         "success" : true
       }, {
         "id" : "aabb",
         "success" : true
       }
     ]
   }

Status Code
-----------

:ref:`Table 5 <kafka-api-180614003__en-us_topic_0128036887_table6231844656>` describes the status code of successful operations. For details about other status codes, see :ref:`Status Code <kafka-api-0034672261>`.

.. _kafka-api-180614003__en-us_topic_0128036887_table6231844656:

.. table:: **Table 5** Status code

   =========== ====================================
   Status Code Description
   =========== ====================================
   200         The topics are successfully deleted.
   =========== ====================================
