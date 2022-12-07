:original_name: kafka_ug_0025.html

.. _kafka_ug_0025:

Resetting the SASL_SSL Password
===============================

Scenario
--------

If you forget the password of a SASL_SSL user created on the **Users** tab page, you can reset the password and use the new password to connect to the Kafka instance.

If you forget the SASL_SSL password set during instance creation, reset the password by following the instructions provided in :ref:`Resetting Kafka Password <kafka-ug-180718001>`.

.. note::

   -  You can reset the SASL_SSL password only if Kafka SASL_SSL has been enabled for the instance.
   -  You can reset the SASL_SSL password only when the instance is in the **Running** state.

Procedure
---------

#. Log in to the management console.
#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the name of the desired Kafka instance.
#. On the **Users** tab page, click **Reset Password** in the row containing the desired user.
#. Enter and confirm a new password, and click **OK**.

   -  If the password is successfully reset, a success message is displayed.
   -  If the password fails to be reset, a failure message is displayed. In this case, reset the password again. If you still fail to reset the password after multiple attempts, contact customer service.

   .. note::

      The system will display a success message only after the password is successfully reset on all brokers.

.. |image1| image:: /_static/images/en-us_image_0000001379301802.png
