:original_name: kafka-ug-200506001.html

.. _kafka-ug-200506001:

Changing Kafka Message Retention Period
=======================================

Aging time is a period that messages in a topic are retained for. Consumers must consume messages before this period ends. Otherwise, the messages will be deleted and can no longer be consumed.

The topic retention period is 72 hours by default, and can be changed later as required. Changing the aging time does not affect services.

You can change the aging time in either of the following ways:

-  By changing the **Aging Time** configuration on the **Topics** page.
-  By changing the value of the **log.retention.hours** parameter on the **Parameters** tab page. For details, see :ref:`Modifying Kafka Instance Configuration Parameters <kafka-ug-0007>`.

The value of the **log.retention.hours** parameter takes effect only if the aging time has not been set for the topic. For example, if the aging time of Topic01 is set to 60 hours and **log.retention.hours** is set to 72 hours, the actual aging time of Topic01 is 60 hours.

Notes and Constraints
---------------------

-  The retention period of single-node instances can be modified only on the **Topics** page.

Modifying the Message Retention Period of a Topic
-------------------------------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select the region where your instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired instance to go to the instance details page.

#. In the navigation pane, choose **Topics**.

#. Modify the topic aging time using either of the following methods:

   -  Select one or more topics and click **Edit Topic** in the upper left corner.
   -  In the row containing the desired topic, click **Edit**.

#. In the **Edit Topic** dialog box, enter the aging time (1-720) and click **OK**.

   View the aging time on the **Topics** page.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
