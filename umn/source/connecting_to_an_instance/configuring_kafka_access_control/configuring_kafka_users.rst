:original_name: kafka-ug-0003.html

.. _kafka-ug-0003:

Configuring Kafka Users
=======================

DMS supports access control list (ACL) for topics. You can differentiate user permissions by granting users different permissions in a topic.

This section describes how to create users, reset the password, and delete users with ciphertext access enabled. For details about how to grant topic permissions for users, see :ref:`Configuring Kafka Topic Permissions <kafka-ug-0002>`.

**The maximum number of users that can be created for a Kafka instance is 20 or 500. Check the console for the actual limit.**

There are two ways to create a user on the console. Accordingly, there are two ways to reset the user's password:

-  Initial user: The user set when ciphertext access is enabled for the first time. If you forget your password, reset it by referring to :ref:`Resetting the Password (for the Initial User) <kafka-ug-0003__section125811843123418>`.
-  Non-initial users: Users created on the **Users** page. If you forget your password, reset it by referring to :ref:`Resetting the User Password (for Non-initial Users) <kafka-ug-0003__section728275161010>`.

Prerequisites
-------------

-  Ciphertext access has been enabled for the Kafka instance.
-  Kafka users can be configured only for Kafka instances in the **Running** state.

Constraints
-----------

-  This function is unavailable for single-node instances.
-  Resetting a user password will interrupt services. Change the user password in the client configuration file or code as soon as possible.

Creating a User
---------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view its details.

#. On the **Users** page, click **Create User**.

#. In the displayed **Create User** dialog box, set the username and password, and click **OK**.

   After the user is created, grant permissions to the user by referring to :ref:`Configuring Kafka Topic Permissions <kafka-ug-0002>`.

.. _kafka-ug-0003__section125811843123418:

Resetting the Password (for the Initial User)
---------------------------------------------

#. Log in to the console.
#. Click |image2| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Reset the password for the initial user in either of the following ways.

   -  Choose **More** > **Reset Kafka Password** in the row containing the desired Kafka instance.
   -  Click the desired Kafka instance to view its details. Choose **More** > **Reset Kafka Password** in the upper left corner.
   -  Click the desired Kafka instance to view its details. On the **Basic Information** page, click **Reset Password** next to **Username** in the **Connection** section.
   -  Click the desired Kafka instance to view its details. On the **Users** page, click **Reset Password** in the row containing the desired user.

#. Enter and confirm a new password, and click **OK**.

   -  If the password is successfully reset, a success message is displayed.
   -  If the password fails to be reset, a failure message is displayed. In this case, reset the password again. If you still fail to reset the password after multiple attempts, contact customer service.

   .. note::

      The system will display a success message only after the password is successfully reset on all brokers.

.. _kafka-ug-0003__section728275161010:

Resetting the User Password (for Non-initial Users)
---------------------------------------------------

#. Log in to the console.
#. Click |image3| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired Kafka instance to view its details.
#. On the **Users** page, click **Reset Password** in the row containing the desired user.
#. Enter and confirm a new password, and click **OK**.

   -  If the password is successfully reset, a success message is displayed.
   -  If the password fails to be reset, a failure message is displayed. In this case, reset the password again. If you still fail to reset the password after multiple attempts, contact customer service.

   .. note::

      The system will display a success message only after the password is successfully reset on all brokers.

Deleting a User
---------------

#. Log in to the console.
#. Click |image4| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired Kafka instance to view its details.
#. Delete a user in either of the following ways:

   -  On the **Users** page, click **Delete** in the row containing the desired user.
   -  On the **Users** page, select one or more users and click **Delete** above the list.

   .. note::

      The initial user set when ciphertext access is enabled for the first time cannot be deleted.

#. In the displayed **Delete User** dialog box, click **OK** to delete the user.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0143929918.png
.. |image3| image:: /_static/images/en-us_image_0143929918.png
.. |image4| image:: /_static/images/en-us_image_0143929918.png
