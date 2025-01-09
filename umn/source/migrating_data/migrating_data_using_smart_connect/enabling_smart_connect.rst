:original_name: kafka_ug_0017.html

.. _kafka_ug_0017:

Enabling Smart Connect
======================

Smart Connect synchronizes data between Kafka and other cloud services (such as OBS) or between two Kafka instances for backup or migration.

Procedure for using Smart Connect:

#. Enable Smart Connect.
#. Create a Smart Connect task.

This section describes how to enable Smart Connect.

.. note::

   This function is unavailable for single-node instances.

Operation Impact
----------------

Enabling Smart Connect creates at least two brokers.

For example, if you enable Smart Connect for a kafka.4u8g.cluster instance, at least two kafka.4u8g brokers will be created for Smart Connect.

Prerequisites
-------------

-  :ref:`A Kafka instance has been created <kafka-ug-180604013>` and is in the **Running** state.
-  **auto.create.groups.enable** is set to **true**. If no, modify it by referring to :ref:`Modifying Kafka Instance Configuration Parameters <kafka-ug-0007>`.

Procedure
---------

#. Log in to the console.
#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Enable Smart Connect using one of the following methods:

   -  In the row containing the desired Kafka instance, choose **More** > **Enable Smart Connect**.
   -  Click the desired Kafka instance to view its details. In the upper right corner, choose **More** > **Enable Smart Connect**.
   -  Click the desired Kafka instance to view its details. Click |image2| next to **Smart Connect**.
   -  Click the desired Kafka instance to view its details. In the navigation pane, choose **Smart Connect**. Click **Enable Smart Connect**.

#. Click |image3|, enable **Smart Connect**, set 2-16 brokers as required, and click **Next**.

   .. note::

      By default, two brokers will be used. If synchronization traffic between two Kafka instances is estimated to be large, for example, greater than 50 MB/s, use more brokers.

#. On the displayed **Enabling Smart Connect for Kafka Instance** page, ensure that **Smart Connect** is enabled and click **Submit**.

Follow-up Operations
--------------------

Proceed to :ref:`Replicating Kafka Instance Data <kafka-ug-0034>`, :ref:`Dumping Kafka Data to Object Storage Service (OBS) <kafka-ug-0035>`, to synchronize data between DMS for Kafka and other cloud services.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0000001314995070.png
.. |image3| image:: /_static/images/en-us_image_0000001191767177.png
