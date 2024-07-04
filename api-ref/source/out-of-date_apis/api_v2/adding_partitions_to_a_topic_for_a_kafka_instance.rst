:original_name: CreatePartition.html

.. _CreatePartition:

Adding Partitions to a Topic for a Kafka Instance
=================================================

Function
--------

This API is used to add partitions to a topic for a Kafka instance.

.. note::

   This API is out-of-date and may not be maintained in the future. Please use the API described in :ref:`Modifying Topics of a Kafka Instance <updateinstancetopic>`.

URI
---

POST /v2/{project_id}/instances/{instance_id}/management/topics/{topic}/partitions-reassignment

.. table:: **Table 1** URI parameters

   +-------------+-----------+--------+---------------------------------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                                                         |
   +=============+===========+========+=====================================================================================================================+
   | project_id  | Yes       | String | Project ID. For details about how to obtain a project ID, see :ref:`Obtaining a Project ID <kafka-api-0036212547>`. |
   +-------------+-----------+--------+---------------------------------------------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                                                        |
   +-------------+-----------+--------+---------------------------------------------------------------------------------------------------------------------+
   | topic       | Yes       | String | Topic name.                                                                                                         |
   +-------------+-----------+--------+---------------------------------------------------------------------------------------------------------------------+

Request
-------

.. table:: **Table 2** Request parameter

   +-----------+-----------+---------+------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Mandatory | Type    | Description                                                                                                                        |
   +===========+===========+=========+====================================================================================================================================+
   | partition | No        | Integer | Total number of partitions after the addition. The value must be larger than current number of partitions. Maximum value: **100**. |
   +-----------+-----------+---------+------------------------------------------------------------------------------------------------------------------------------------+

Response
--------

None.

Example Request
---------------

Adding partitions to a topic.

.. code-block:: text

   POST https://{endpoint}/v2/{project_id}/instances/{instance_id}/management/topics/{topic}/partitions-reassignment

   {
     "partition" : 3
   }

Example Response
----------------

None.

Status Code
-----------

=========== ==============================
Status Code Description
=========== ==============================
204         Partitions added successfully.
=========== ==============================

Error Code
----------

For details, see :ref:`Error Codes <errorcode>`.
