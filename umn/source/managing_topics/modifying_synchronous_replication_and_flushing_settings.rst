:original_name: kafka_ug_0022.html

.. _kafka_ug_0022:

Modifying Synchronous Replication and Flushing Settings
=======================================================

Synchronous replication: A message is returned to the client only after the message creation request has been received and the message has been acknowledged by all replicas.

Synchronous flushing: A message is immediately flushed to disk once created.

-  Enabled: A message is immediately flushed to disk once it is created, resulting in higher reliability.
-  Disabled: A message is stored in the memory instead of being immediately flushed to disk once created.

The following procedure describes how to modify synchronous replication and synchronous flushing settings on the console.

Procedure
---------

#. Log in to the management console.
#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired Kafka instance to view the instance details.
#. Click the **Topics** tab.
#. Use either of the following methods to modify synchronous replication and synchronous flushing settings:

   -  Select one or more topics and click **Edit Topic** above the topic list.
   -  In the row that contains the topic whose synchronous replication and flushing settings are to be modified, click **Edit**.

#. In the **Edit Topic** dialog box, enable or disable synchronous replication and synchronous flushing, and click **OK**.

   -  To enable them, click |image2|.
   -  To disable them, click |image3|.

   .. note::

      -  If there is only one replica, synchronous replication cannot be enabled.
      -  After enabling synchronous replication, set **acks** to **all** or **-1** on the client. Otherwise, this function will not take effect.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0000001191767177.png
.. |image3| image:: /_static/images/en-us_image_0000001283221910.png
