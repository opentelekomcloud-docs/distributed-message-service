:original_name: kafka-ug-0003.html

.. _kafka-ug-0003:

Creating a SASL_SSL User
========================

DMS supports ACL permission management for topics. You can differentiate the operations that different users are allowed to perform on a topic by granting the users different permissions.

This section describes how to create a SASL_SSL user after SASL_SSL is enabled for a Kafka instance. For details about how to grant user permissions, see :ref:`Granting Permissions to a SASL_SSL User <kafka-ug-0002>`.

Prerequisites
-------------

SASL_SSL has been enabled when you create the Kafka instance.

Procedure
---------

#. Log in to the management console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view the instance details.

#. On the **Users** tab page, click **Create User**.

#. In the displayed **Create User** dialog box, set the username and password, and click OK.

   After the SASL_SSL user is created, grant permissions to the user by referring to :ref:`Granting Permissions to a SASL_SSL User <kafka-ug-0002>`.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
