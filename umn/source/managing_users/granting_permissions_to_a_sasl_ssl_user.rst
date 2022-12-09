:original_name: kafka-ug-0002.html

.. _kafka-ug-0002:

Granting Permissions to a SASL_SSL User
=======================================

DMS supports ACL permission management for topics. You can differentiate the operations that different users are allowed to perform on a topic by granting the users different permissions.

This section describes how to grant topic permissions to a SASL_SSL user. For details about how to create a SASL_SSL user, see :ref:`Creating a SASL_SSL User <kafka-ug-0003>`.

If no SASL_SSL user is granted any permission for a topic, all users can subscribe to or publish messages to the topic.

If one or more SASL_SSL users are granted permissions for a topic, only the authorized users can subscribe to or publish messages to the topic.

Prerequisites
-------------

-  SASL_SSL has been enabled when you create the Kafka instance.
-  (Optional) A SASL_SSL user has been created. For details, see :ref:`Creating a SASL_SSL User <kafka-ug-0003>`.


Granting Permissions to a SASL_SSL User
---------------------------------------

#. Log in to the management console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view the instance details.

#. In the navigation pane, choose the **Topics** tab.

#. In the row that contains the topic for which you want to configure user permissions, click **Grant User Permission**.

   In the upper part of the **Grant User Permission** dialog box, the topic information is displayed, including the topic name, number of partitions, aging time, number of replicas, and whether synchronous flushing is enabled. In the middle part, you can use the search box to search for a user if there are many SASL_SSL users. In the **Users** area, the list of created SASL_SSL users is displayed. In the **Selected** area, you can grant permissions to the SASL_SSL users.

#. In the **Users** area of the **Grant User Permission** dialog box, select target users. In the **Selected** area, configure permissions (**Subscribe**, **Publish**, and **Publish/Subscribe**) for the users.

   .. _kafka-ug-0002__fig15529113214543:

   .. figure:: /_static/images/en-us_image_0000001380945917.png
      :alt: **Figure 1** Granting user permissions

      **Figure 1** Granting user permissions

   As shown in :ref:`Figure 1 <kafka-ug-0002__fig15529113214543>`, only the **test**, **send**, and **receive** users can subscribe to or publish messages to topic-01. The **send_receive** user cannot subscribe to or publish messages to topic-01.

#. Click **OK**.

   On the **Topics** tab page, click |image2| next to the topic name to view the authorized users and their permissions.


   .. figure:: /_static/images/en-us_image_0000001329906052.png
      :alt: **Figure 2** Viewing authorized users and their permissions

      **Figure 2** Viewing authorized users and their permissions

(Optional) Removing Permissions from a SASL_SSL User
----------------------------------------------------

#. Log in to the management console.
#. Click |image3| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired Kafka instance to view the instance details.
#. In the navigation pane, choose the **Topics** tab.
#. In the row that contains the topic for which you want to remove user permissions, click **Grant User Permission**.
#. In the **Selected** area of the displayed **Grant User Permission** dialog box, locate the row that contains the SASL_SSL user whose permissions are to be removed, click **Delete**, and click **OK**.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0000001160594580.png
.. |image3| image:: /_static/images/en-us_image_0143929918.png
