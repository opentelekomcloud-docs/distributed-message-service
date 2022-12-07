:original_name: kafka-ug-180718001.html

.. _kafka-ug-180718001:

Resetting Kafka Password
========================

Scenario
--------

You can reset the SASL_SSL password for accessing a Kafka instance by resetting Kafka password if you forget it.

.. note::

   -  You can reset the Kafka password only if Kafka SASL_SSL has been enabled for the instance.
   -  You can reset the Kafka password only when the instance is in the **Running** state.

Procedure
---------

#. Log in to the management console.
#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Reset the Kafka instance password using either of the following methods:

   -  Choose **More** > **Reset Kafka Password** in the row containing the desired Kafka instance.
   -  Click the desired Kafka instance to view its details. On the **Basic Information** tab page, click **Reset Password** next to **Username** in the **Connection** section.
   -  Click the desired Kafka instance to view its details. On the **Users** tab page, click **Reset Password** in the row containing the desired user.

#. In the **Reset Kafka Password** dialog box, enter and confirm a new password, and click **OK**.

   -  If the password is successfully reset, a success message is displayed.
   -  If the password fails to be reset, a failure message is displayed. Reset the password again. If you still fail to reset the password after multiple attempts, contact customer service.

   .. note::

      The system will display a success message only after the password is successfully reset on all brokers.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
