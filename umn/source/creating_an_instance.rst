:original_name: dms-ug-180604013.html

.. _dms-ug-180604013:

Creating an Instance
====================

Scenario
--------

Kafka instances are physically isolated and exclusively occupied by each tenant. You can customize the computing capabilities and storage space of an instance based on service requirements.

Before You Start
----------------

-  Before creating a Kafka instance, ensure that a VPC configured with security groups and subnets is available.
-  (Optional) If you want to access a Kafka instance over a public network, prepare an elastic IP address (EIP) in advance.
-  (Optional) If you need to encrypt the disk, prepare a KMS key in advance.

Procedure
---------

#. Log in to the management console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the same region as your application service.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click **Create Instance** in the upper right corner of the page.

   By default, you can create a maximum of 100 Kafka instances for each project. To create more instances, contact customer service to increase your quota.

#. Specify **Region**, **Project**, and **AZ**.

#. Enter an instance name.

#. Configure the following instance parameters:

   a. **Version**: Kafka v1.1.0, v2.3.0, and v2.7 are supported. v2.7 is recommended. **The version cannot be changed once the instance is created.**

   b. **CPU Architecture**: The x86 architecture is supported.

   c. **Flavor**: Select a bandwidth based on the estimated service traffic.

      You can view the broker quantity and flavor, the maximum number of partitions allowed, and number of consumer groups recommended for each bandwidth option.

      The **Maximum Partitions** parameter indicates the maximum number of partitions that can be created for a Kafka instance. If the total number of partitions of all topics exceeds this threshold, topic creation will fail.

   d. **Storage Space**: Disk type and total disk space for storing the instance data. **The disk type cannot be changed once the instance is created.**

      The storage space is the total space to be consumed by all replicas. Specify the storage space based on the expected service message size and the number of replicas. For example, if the required disk size to store the data for the retention period is 100 GB, the disk capacity must be at least: 100 GB x Number of replicas + 100 GB (reserved space).

      Disks are formatted when an instance is created. As a result, the actual available disk space is 93% to 95% of the total disk space.

      -  100 MB/s bandwidth: The value range of **Storage Space** is 600-90,000 GB.
      -  300 MB/s bandwidth: The value range of **Storage Space** is 1200-90,000 GB.
      -  600 MB/s bandwidth: The value range of **Storage Space** is 2400-90,000 GB.
      -  1200 MB/s bandwidth: The value range of **Storage Space** is 4800-90,000 GB.

      .. note::

         -  High I/O + 100 MB/s bandwidth: If the average message size is 1 KB, the transactions per second (TPS) can reach 100,000 in high throughput scenarios and 60,000 in synchronous replication scenarios.
         -  High I/O + 300 MB/s bandwidth: If the average message size is 1 KB, the TPS can reach 300,000 in high throughput scenarios and 150,000 in synchronous replication scenarios.
         -  Ultra-high I/O + 100 MB/s bandwidth: If the average message size is 1 KB, the TPS can reach 100,000 in high throughput scenarios and 80,000 in synchronous replication scenarios.
         -  Ultra-high I/O + 300 MB/s bandwidth: If the average message size is 1 KB, the TPS can reach 300,000 in high throughput scenarios and 200,000 in synchronous replication scenarios.
         -  Ultra-high I/O + 600 MB/s bandwidth: If the average message size is 1 KB, the TPS can reach 600,000 in high throughput scenarios and 300,000 in synchronous replication scenarios.
         -  Ultra-high I/O + 1200 MB/s bandwidth: If the average message size is 1 KB, the TPS can reach 1,200,000 in high throughput scenarios and 400,000 in synchronous replication scenarios.

   e. **Disk Encryption**: Specify whether to enable disk encryption. Enabling disk encryption improves data security. Disk encryption depends on Key Management Service (KMS). If you enable disk encryption, select a KMS key. **This parameter cannot be modified once the instance is created.**

   f. **Capacity Threshold Policy**: policy used when the disk usage reaches the threshold. The capacity threshold is 95%.

      -  **Automatically delete**: Messages can be created and retrieved, but 10% of the earliest messages will be deleted to ensure sufficient disk space. This policy is suitable for scenarios where no service interruption can be tolerated. Data may be lost.
      -  **Stop production**: New messages cannot be created, but existing messages can still be retrieved. This policy is suitable for scenarios where no data loss can be tolerated.

#. Configure the instance network parameters.

   -  Select a VPC and a subnet.

      A VPC provides an isolated virtual network for your Kafka instances. You can configure and manage the network as required.

      .. note::

         After the Kafka instance is created, its VPC and subnet cannot be changed.

   -  Select a security group.

      A security group is a set of rules for accessing a Kafka instance. You can click **Manage Security Group** to view or create security groups on the network console.

#. Click **Advanced Settings** to configure more parameters.

   a. Configure public access.

      Public access is disabled by default. You can enable or disable it as required.

      After public access is enabled, configure an IPv4 EIP for each broker.

   b. Configure **Kafka SASL_SSL**.

      This parameter indicates whether to enable SSL authentication when a client connects to the instance. If you enable **Kafka SASL_SSL**, data will be encrypted before transmission to enhance security.

      **Kafka SASL_SSL** is disabled by default. You can enable or disable it as required. **This setting cannot be changed after the instance is created.** If you want to use a different setting, you must create a new instance.

      If you enable **Kafka SASL_SSL**, you must also set the username and password for accessing the instance.

   c. Configure **Automatic Topic Creation**.

      This setting is disabled by default. You can enable or disable it as required.

      If automatic topic creation is enabled, the system automatically creates a topic when a message is created in or retrieved from a topic that does not exist. This topic has the following default settings: 3 partitions, 3 replicas, aging time 72 hours, and synchronous replication and flushing disabled.

      After you change the value of the **log.retention.hours**, **default.replication.factor**, or **num.partitions** parameter, automatically created topics later use the new value. For example, if **num.partitions** is set to **5**, an automatically created topic will have the following settings: 5 partitions, 3 replicas, aging time 72 hours, and synchronous replication and flushing disabled.

   d. Specify **Tags**.

      Tags are used to identify cloud resources. When you have many cloud resources of the same type, you can use tags to classify them by dimension (for example, use, owner, or environment).

      -  If you have predefined tags, select a predefined pair of tag key and value. Click **View predefined tags**. On the Tag Management Service (TMS) console, view predefined tags or create tags.
      -  You can also create new tags by specifying **Tag key** and **Tag value**.

      Up to 20 tags can be added to each Kafka instance. For details about the requirements on tags, see :ref:`Managing Instance Tags <tagmanagement>`.

   e. Enter a description of the instance.

#. Click **Create**.

#. Confirm the instance information, and click **Submit**.

#. Return to the instance list and check whether the Kafka instance has been created.

   It takes 3 to 15 minutes to create an instance. During this period, the instance status is **Creating**.

   -  If the instance is created successfully, its status changes to **Running**.
   -  If the instance fails to be created, view **Instance Creation Failures**. Delete the instance by referring to :ref:`Deleting an Instance <kafka-ug-180604016>` and create another instance. If the instance creation fails again, contact customer service.

      .. note::

         Instances that fail to be created do not occupy other resources.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
