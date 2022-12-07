:original_name: kafka-ug-180604014.html

.. _kafka-ug-180604014:

Viewing an Instance
===================

Scenario
--------

View detailed information about a Kafka instance on the DMS console, for example, the IP addresses and port numbers for accessing the instance.

Procedure
---------

#. Log in to the management console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Search for a Kafka instance by tag, status, name, ID, or connection address. :ref:`Table 1 <kafka-ug-180604014__table5086721717534>` describes the various possible statuses of a Kafka instance.

   .. _kafka-ug-180604014__table5086721717534:

   .. table:: **Table 1** Kafka instance status description

      +-----------------------------------+------------------------------------------------------------------------------------+
      | Status                            | Description                                                                        |
      +===================================+====================================================================================+
      | Creating                          | The instance is being created.                                                     |
      +-----------------------------------+------------------------------------------------------------------------------------+
      | Running                           | The instance is running properly.                                                  |
      |                                   |                                                                                    |
      |                                   | Only instances in the **Running** state can provide services.                      |
      +-----------------------------------+------------------------------------------------------------------------------------+
      | Faulty                            | The instance is not running properly.                                              |
      +-----------------------------------+------------------------------------------------------------------------------------+
      | Starting                          | The status between **Frozen** and **Running**.                                     |
      +-----------------------------------+------------------------------------------------------------------------------------+
      | Restarting                        | The instance is being restarted.                                                   |
      +-----------------------------------+------------------------------------------------------------------------------------+
      | Changing                          | The instance specifications or public access configurations are being modified.    |
      +-----------------------------------+------------------------------------------------------------------------------------+
      | Change failed                     | The instance specifications or public access configurations failed to be modified. |
      +-----------------------------------+------------------------------------------------------------------------------------+
      | Frozen                            | The instance is frozen.                                                            |
      +-----------------------------------+------------------------------------------------------------------------------------+
      | Freezing                          | The status between **Running** and **Frozen**.                                     |
      +-----------------------------------+------------------------------------------------------------------------------------+
      | Upgrading                         | The instance is being upgraded.                                                    |
      +-----------------------------------+------------------------------------------------------------------------------------+
      | Rolling back                      | The instance is being rolled back.                                                 |
      +-----------------------------------+------------------------------------------------------------------------------------+

#. Click the name of the desired Kafka instance and view detailed information about the instance on the **Basic Information** tab page.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
