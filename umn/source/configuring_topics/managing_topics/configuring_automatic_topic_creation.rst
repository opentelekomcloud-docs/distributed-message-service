:original_name: kafka_ug_0043.html

.. _kafka_ug_0043:

Configuring Automatic Topic Creation
====================================

**Automatic Topic Creation** indicates that a topic will be automatically created when a message is produced in or consumed from a topic that does not exist. By default, the topic has parameters listed in :ref:`Table 1 <kafka_ug_0043__table101881121219>`.

After you change the value of the **log.retention.hours** (retention period), **default.replication.factor** (replica quantity), or **num.partitions** (partition quantity) parameter, the value will be used in later topics that are automatically created. For example, assume that **num.partitions** is changed to 5, an automatically created topic has parameters listed in :ref:`Table 1 <kafka_ug_0043__table101881121219>`.

.. _kafka_ug_0043__table101881121219:

.. table:: **Table 1** Topic parameters

   ========================= ============= ==============
   Parameter                 Default Value Modified Value
   ========================= ============= ==============
   Partitions                3             5
   Replicas                  3             3
   Aging Time (h)            72            72
   Synchronous Replication   Disabled      Disabled
   Synchronous Flushing      Disabled      Disabled
   Message Timestamp         CreateTime    CreateTime
   Max. Message Size (bytes) 10,485,760    10,485,760
   ========================= ============= ==============

Procedure
---------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view its details.

#. In the **Instance Information** area, click |image2| or |image3| next to **Automatic Topic Creation**. The **Confirm** dialog box is displayed.

   .. note::

      **Enabling or disabling automatic topic creation may cause instance restarts.**

#. Click **OK**.

   You can view the execution status of the task on the **Background Tasks** page.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0000001283221910.png
.. |image3| image:: /_static/images/en-us_image_0000001191767177.png
