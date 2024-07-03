:original_name: kafka-ug-0002.html

.. _kafka-ug-0002:

Configuring Kafka Topic Permissions
===================================

DMS supports access control list (ACL) for topics. You can differentiate user permissions by granting users different permissions in a topic.

This section describes how to grant topic permissions to users after ciphertext access is enabled for Kafka instances. For details about how to create a user, see :ref:`Configuring Kafka Users <kafka-ug-0003>`.

.. note::

   This function is unavailable for single-node instances.

Constraints
-----------

-  If no user is granted any permission for a topic and **allow.everyone.if.no.acl.found** is set to **true**, all users can subscribe to or publish messages to the topic.
-  If **allow.everyone.if.no.acl.found** is set to **false**, only the authorized users can subscribe to or publish messages to the topic. The value of **allow.everyone.if.no.acl.found** can be :ref:`modified <kafka-ug-0007>`.
-  If one or more users are granted permissions for a topic, only the authorized users can subscribe to or publish messages to the topic.
-  If both the default and individual user permissions are configured for a topic, the union of the permissions is used.

Prerequisites
-------------

-  Ciphertext access has been enabled.
-  (Optional) A user has been created. For details, see :ref:`Configuring Kafka Users <kafka-ug-0003>`.

Configuring Topic Permissions
-----------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view the instance details.

#. In the navigation pane, choose **Topics**.

#. In the row containing the desired topic, click **Grant User Permission**.

   In the upper part of the **Grant User Permission** dialog box, the topic information is displayed, including the topic name, number of partitions, aging time, number of replicas, and whether synchronous flushing and replication are enabled. You can enable **Default permissions** to grant the same permissions for all users. You can use the search box to search for a user if there are many users. In the **Users** area, the list of created users is displayed. In the **Selected** area, grant permissions to the users.

#. Grant topic permissions to users.

   -  To grant the same permissions to all users, select **Default permissions** and then select permissions. As shown in the following figure, all users have the permission to publish messages to this topic.


      .. figure:: /_static/images/en-us_image_0000001803832641.png
         :alt: **Figure 1** Granting the same permissions to all users

         **Figure 1** Granting the same permissions to all users

   -  To grant different permissions to different users, do not select **Default permissions**. In the **Users** area of the **Grant User Permission** dialog box, select target users. In the **Selected** area, configure permissions (**Subscribe**, **Publish**, or **Publish/Subscribe**) for the users. As shown in the following figure, only the **test**, **send**, and **receive** users can subscribe to or publish messages to this topic. The **send_receive** user cannot subscribe to or publish messages to this topic.


      .. figure:: /_static/images/en-us_image_0000001803837729.png
         :alt: **Figure 2** Granting permissions to individual users

         **Figure 2** Granting permissions to individual users

   **If both the default and individual user permissions are configured for a topic, the union of the permissions is used.** As shown in the following figure, the **test** and **receive** users can subscribe to and publish messages to this topic.


   .. figure:: /_static/images/en-us_image_0000001757003050.png
      :alt: **Figure 3** Granting topic permissions to users

      **Figure 3** Granting topic permissions to users

#. Click **OK**.

   On the **Topics** tab page, click |image2| next to the topic name to view the authorized users and their permissions.


   .. figure:: /_static/images/en-us_image_0000001803846097.png
      :alt: **Figure 4** Viewing authorized users and their permissions

      **Figure 4** Viewing authorized users and their permissions

(Optional) Deleting Topic Permissions
-------------------------------------

#. Log in to the console.
#. Click |image3| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired Kafka instance to view the instance details.
#. In the navigation pane, choose **Topics**.
#. In the row containing the desired topic, click **Grant User Permission**.
#. In the **Selected** area of the displayed **Grant User Permission** dialog box, locate the row that contains the user whose permissions are to be removed, click **Delete**, and click **OK**.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0000001160594580.png
.. |image3| image:: /_static/images/en-us_image_0143929918.png
