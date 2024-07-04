:original_name: kafka-ug-0041.html

.. _kafka-ug-0041:

Creating a Kafka Consumer Group
===============================

Create a consumer group on the console.

**auto.create.groups.enable**: a consumer group is automatically created when a consumer attempts to enter a group that does not exist.

-  This operation is optional when **auto.create.groups.enable** is **true** in :ref:`Configuring Parameters <kafka-ug-0007>`.
-  A consumer group is required before consuming messages when **auto.create.groups.enable** is **false** in :ref:`Configuring Parameters <kafka-ug-0007>`. Otherwise, consumption will fail.

.. note::

   -  If **auto.create.groups.enable** is set to **true**, the consumer group status is **EMPTY**, and no offset has been submitted, the system automatically deletes the consumer group 10 minutes later.
   -  If **auto.create.groups.enable** is set to **false**, the system does not automatically delete consumer groups. You can manually delete them.
   -  If a consumer group has never committed an offset, the group will be deleted after the Kafka instance restarts.
   -  Creating a consumer group on the console does not require instance restart.


Creating a Kafka Consumer Group
-------------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view the instance details.

#. In the navigation pane, choose **Consumer Groups**.

#. Click **Create Consumer Group**.

#. Set consumer group parameters by referring to :ref:`Table 1 <kafka-ug-0041__table1228103855815>` and click **OK**.

   .. _kafka-ug-0041__table1228103855815:

   .. table:: **Table 1** Consumer group parameters

      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                         |
      +===================================+=====================================================================================================================================================+
      | Consumer Group Name               | Enter 3 to 64 characters, starting with a letter or underscore (_). Use only letters, digits, periods (.), hyphens (-), and underscores (_).        |
      |                                   |                                                                                                                                                     |
      |                                   | If a consumer group name starts with a special character, for example, an underscore (_) or a number sign (#), monitoring data cannot be displayed. |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+

   View the new consumer group in the consumer group list.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
