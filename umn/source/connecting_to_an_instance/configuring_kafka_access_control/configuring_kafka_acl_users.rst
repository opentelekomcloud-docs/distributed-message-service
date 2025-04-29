:original_name: kafka-ug-0003.html

.. _kafka-ug-0003:

Configuring Kafka ACL Users
===========================

Kafka instances with ciphertext access enabled support access control list (ACL) for topics. You can differentiate user permissions by granting users different permissions in a topic.

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

-  Single-node instances do not support user creation, user password reset, or user deletion.
-  Resetting a user password will interrupt services. Change the user password in the client configuration file or code as soon as possible.

Creating a User
---------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired instance to go to the instance details page.

#. On the **Users** page, click **Create User**.

#. Set user information by referring to :ref:`Configuring Kafka ACL Users <kafka-ug-0003>`.

   .. table:: **Table 1** User creation parameters

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                              |
      +===================================+==========================================================================================================================================================================================================================+
      | Username                          | The username used to access a Kafka instance, you can customize a name that complies with the rules: 4-64 characters; starts with a letter; can contain only letters, digits, hyphens (-), and underscores (_).          |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Password                          | The password used to access a Kafka instance. A password must meet the following requirements:                                                                                                                           |
      |                                   |                                                                                                                                                                                                                          |
      |                                   | -  Contains 8 to 32 characters.                                                                                                                                                                                          |
      |                                   | -  Contains at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters \`~! @#$ ``%^&*()-_=+\|[{}];:'",<.>?`` and spaces, and cannot start with a hyphen (-). |
      |                                   | -  Cannot be the username spelled forward or backward.                                                                                                                                                                   |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

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
#. In the navigation pane, choose **Users**.
#. Delete a user in either of the following ways:

   -  In the row containing the desired user, click **Delete**.
   -  Select one or more users and click **Delete** above the list.

   .. note::

      The initial user set when ciphertext access is enabled for the first time cannot be deleted.

#. In the displayed **Delete User** dialog box, click **OK** to delete the user.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0143929918.png
.. |image3| image:: /_static/images/en-us_image_0143929918.png
.. |image4| image:: /_static/images/en-us_image_0143929918.png
