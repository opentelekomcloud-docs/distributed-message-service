:original_name: kafka-ug-200506001.html

.. _kafka-ug-200506001:

Modifying Topic Aging Time
==========================

Aging time is a period that messages in the topic are retained for. Consumers must retrieve messages before this period ends. Otherwise, the messages will be deleted and can no longer be retrieved.

After creating a topic, you can change its aging time based on service requirements. Changing the aging time does not affect services. The default aging time is 72 hours.

You can change the aging time in either of the following ways:

-  By editing the topic on the **Topics** tab page
-  By changing the value of the **log.retention.hours** parameter on the **Parameters** tab page. For details, see :ref:`Modifying Kafka Parameters <kafka-ug-0007>`.

.. note::

   The **log.retention.hours** parameter takes effect only for topics that have no aging time configured. If there is aging time configured for a topic, it overrides the **log.retention.hours** parameter. For example, if the aging time of Topic01 is set to 60 hours and **log.retention.hours** is set to 72 hours, the actual aging time of Topic01 is 60 hours.

Procedure
---------

#. Log in to the management console.
#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired Kafka instance to view the instance details.
#. Click the **Topics** tab.
#. Modify the topic aging time using either of the following methods:

   -  Select one or more topics and click **Edit Topic** in the upper left corner.
   -  In the row containing the desired topic, click **Edit**.

#. In the **Edit Topic** dialog box, enter the aging time and click **OK**.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
