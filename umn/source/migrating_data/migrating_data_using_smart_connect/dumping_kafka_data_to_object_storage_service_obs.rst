:original_name: kafka-ug-0035.html

.. _kafka-ug-0035:

Dumping Kafka Data to Object Storage Service (OBS)
==================================================

Create a Smart Connect task to dump Kafka instance data to OBS for message data backup.

.. note::

   Data in the source Kafka instance is synchronized to the dumping file in real time.

Notes and Constraints
---------------------

-  This function is unavailable for single-node Kafka 3.x instances.
-  A maximum of 18 Smart Connect tasks can be created for an instance.
-  After a Smart Connect task is created, task parameters cannot be modified.

Prerequisites
-------------

-  You have :ref:`enabled Smart Connect <kafka_ug_0017>`.
-  A Kafka instance has been created and is in the **Running** state.
-  The OBS bucket must be created in the same region as the Kafka instance.

Procedure
---------

#. Log in to the console.
#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired Kafka instance to view its details.
#. In the navigation pane, choose **Smart Connect**.
#. On the displayed page, click **Create Task**.
#. For **Task Name**, enter a unique Smart Connect task name. Naming rules: 4-64 characters and only letters, digits, hyphens (-), or underscores (_).
#. For **Task Type**, select **Dumping**.
#. For **Start Immediately**, specify whether to execute the task immediately after the task is created. By default, the task is executed immediately. If you disable this option, you can enable it later in the task list.
#. In the **Source** area, retain the default setting.
#. In the **Topics** area, set parameters based on the following table.

   .. table:: **Table 1** Topic parameters

      +--------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter          | Description                                                                                                                                 |
      +====================+=============================================================================================================================================+
      | Regular expression | A regular expression is used to subscribe to topics whose messages you want to dump.                                                        |
      +--------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
      | Enter/Select       | Enter or select the names of the topics to be dumped. Separate them with commas (,). **A maximum of 20 topics can be entered or selected.** |
      +--------------------+---------------------------------------------------------------------------------------------------------------------------------------------+

#. In the **Target** area, set parameters based on the following table.

   .. table:: **Table 2** Target parameters

      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                 |
      +===================================+=============================================================================================================================================================================================================================+
      | Offset                            | Options:                                                                                                                                                                                                                    |
      |                                   |                                                                                                                                                                                                                             |
      |                                   | -  **Minimum offset**: dumping the earliest data                                                                                                                                                                            |
      |                                   | -  **Maximum offset**: dumping the latest data                                                                                                                                                                              |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Dumping Period (s)                | Interval for periodically dumping data. The time unit is second and the default interval is 300 seconds.                                                                                                                    |
      |                                   |                                                                                                                                                                                                                             |
      |                                   | No package files will be generated if there is no data within an interval.                                                                                                                                                  |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | AK                                | Access key ID.                                                                                                                                                                                                              |
      |                                   |                                                                                                                                                                                                                             |
      |                                   | For details about how to obtain the AK, see `Access Keys <https://docs.otc.t-systems.com/en-us/usermanual/ac/en-us_topic_0046606340.html>`__.                                                                               |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | SK                                | Secret access key used together with the access key ID.                                                                                                                                                                     |
      |                                   |                                                                                                                                                                                                                             |
      |                                   | For details about how to obtain the SK, see `Access Keys <https://docs.otc.t-systems.com/en-us/usermanual/ac/en-us_topic_0046606340.html>`__.                                                                               |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Dumping Address                   | The OBS bucket used to store the topic data.                                                                                                                                                                                |
      |                                   |                                                                                                                                                                                                                             |
      |                                   | -  **Select**: You can select an existing OBS bucket from the drop-down list or click **Create Dumping Address** to create an OBS bucket.                                                                                   |
      |                                   | -  **Enter**: You can enter an existing OBS bucket or click **Create Dumping Address** to create an OBS bucket. **The OBS bucket to be entered must be in the same region as the Kafka instance.**                          |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Dumping Directory                 | Directory for storing topic files dumped to OBS. Use slashes (/) to separate directory levels.                                                                                                                              |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Time Directory Format             | Data is saved to a hierarchical time directory in the dumping directory. For example, if the time directory is accurate to day, the directory will be in the format of *bucket name*/*file directory*/*year*/*month*/*day*. |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Record Separator                  | Select a separator to separate OBS dumping records.                                                                                                                                                                         |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Use Storage Key                   | Specifies whether to dump keys.                                                                                                                                                                                             |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      Do not use the key of a message as the dumping file name.

#. Click **Create**. The Smart Connect task list page is displayed. The message "Task *xxx* was created successfully." is displayed in the upper right corner of the page.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
