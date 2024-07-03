:original_name: kafka-ug-180604013.html

.. _kafka-ug-180604013:

Creating a Kafka Instance
=========================

Scenario
--------

Kafka instances are tenant-exclusive, and physically isolated in deployment. You can customize the computing capabilities and storage space of a Kafka instance as required.

Prerequisites
-------------

Before creating a Kafka instance, prepare the resources listed in :ref:`Table 1 <kafka-ug-180604013__table121034152119>`.

.. _kafka-ug-180604013__table121034152119:

.. table:: **Table 1** Kafka resources

   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Resource              | Requirement                                                                                                                                                     | Operations                                                                                                                                                                                                                                                                                                                                         |
   +=======================+=================================================================================================================================================================+====================================================================================================================================================================================================================================================================================================================================================+
   | VPC and subnet        | You need to configure a VPC and subnet for the Kafka instance as required. You can use the current account's existing VPC and subnet, or create new ones.       | For details on how to create a VPC and a subnet, see `Creating a VPC <https://docs.otc.t-systems.com/en-us/usermanual/vpc/en-us_topic_0013935842.html>`__. If you need to create and use a new subnet in an existing VPC, see `Creating a Subnet for the VPC <https://docs.otc.t-systems.com/en-us/usermanual/vpc/en-us_topic_0013748726.html>`__. |
   |                       |                                                                                                                                                                 |                                                                                                                                                                                                                                                                                                                                                    |
   |                       | Note: VPCs must be created in the same region as the Kafka instance.                                                                                            |                                                                                                                                                                                                                                                                                                                                                    |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Security group        | Different Kafka instances can use the same or different security groups.                                                                                        | For details on how to create a security group, see `Creating a Security Group <https://docs.otc.t-systems.com/en-us/usermanual/vpc/en-us_topic_0013748715.html>`__. For details on how to add rules to a security group, see `Adding a Security Group Rule <https://docs.otc.t-systems.com/en-us/usermanual/vpc/en-us_topic_0030969470.html>`__.   |
   |                       |                                                                                                                                                                 |                                                                                                                                                                                                                                                                                                                                                    |
   |                       | Before accessing a Kafka instance, configure security groups based on the access mode. For details, see :ref:`Table 2 <kafka-ug-180604012__table161395381402>`. |                                                                                                                                                                                                                                                                                                                                                    |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | EIP                   | To create a Kafka instance and access it over a public network, create EIPs in advance.                                                                         | For details about how to create an EIP, see `Assigning an EIP <https://docs.otc.t-systems.com/en-us/usermanual/eip/eip_0002.html>`__.                                                                                                                                                                                                              |
   |                       |                                                                                                                                                                 |                                                                                                                                                                                                                                                                                                                                                    |
   |                       | Note the following when creating EIPs:                                                                                                                          |                                                                                                                                                                                                                                                                                                                                                    |
   |                       |                                                                                                                                                                 |                                                                                                                                                                                                                                                                                                                                                    |
   |                       | -  The EIPs must be created in the same region as the Kafka instance.                                                                                           |                                                                                                                                                                                                                                                                                                                                                    |
   |                       | -  The number of EIPs must be the same as the number of Kafka instance brokers.                                                                                 |                                                                                                                                                                                                                                                                                                                                                    |
   |                       | -  **The Kafka console cannot identify IPv6 EIPs.**                                                                                                             |                                                                                                                                                                                                                                                                                                                                                    |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | KMS key               | To encrypt the disk for a Kafka instance, prepare a KMS key.                                                                                                    | For details about how to create a KMS key, see `Creating a Key <https://docs.otc.t-systems.com/en-us/usermanual/kms/dew_01_0178.html>`__.                                                                                                                                                                                                          |
   |                       |                                                                                                                                                                 |                                                                                                                                                                                                                                                                                                                                                    |
   |                       | The KMS key must be created in the same region as the Kafka instance.                                                                                           |                                                                                                                                                                                                                                                                                                                                                    |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+


Creating a Kafka Instance
-------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   Select a region near you to ensure the lowest latency possible.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click **Create Instance** in the upper right corner of the page.

#. Specify **Region**, **Project**, and **AZ**.

   Select one AZ or at least three AZs.

#. Enter an **Instance Name**.

   You can customize a name that complies with the rules: 4-64 characters; starts with a letter; can contain only letters, digits, hyphens (-), and underscores (_).

#. Select an **Enterprise Project**.

   This parameter is for enterprise users. An enterprise project manages cloud resources. The enterprise project management service unifies cloud resources in projects, and resources and members in a project. The default project is **default**.

#. Configure the following instance parameters:

   **Specifications**: Select **Cluster** or **Single-node**.

   -  If you select **Cluster**, specify the version, broker flavor and quantity, disk type, and storage space to be supported by the cluster Kafka instance as required. Cluster instances support Kafka versions 2.3.0, 2.7, and 3.x.
   -  Single-node: Create a Kafka 2.7 instance with one broker. For details about single-node instances, see :ref:`Comparing Single-node and Cluster Kafka Instances <kafka-pd-0052>`.

   **If you select Cluster, specify the version, broker flavor and quantity, disk type, and storage space to be supported by the Kafka instance as required.**

   a. **Version**: Cluster instances support Kafka 2.3.0, 2.7, and 3.x. **The version cannot be changed once the instance is created.**

   b. **CPU Architecture**: The x86 architecture is supported.

   c. **Broker Flavor**: Select a broker flavor that best fit your needs.

      Maximum number of partitions per broker x Number of brokers = Maximum number of partitions of an instance. If the total number of partitions of all topics exceeds the upper limit of partitions, topic creation fails.

   d. For **Brokers**, specify the broker quantity. A 3.x instance can only have three brokers (not changeable).

   e. **Storage space per broker**: Disk type and size for storing the instance data.

      **The disk type cannot be changed once the Kafka instance is created.**

      The storage space is consumed by message replicas, logs, and metadata. Specify the storage space based on the expected service message size, the number of replicas, and the reserved disk space. Each Kafka broker reserves 33 GB disk space for storing logs and metadata.

      Disks are formatted when an instance is created. As a result, the actual available disk space is 93% to 95% of the total disk space.

      The disk supports high I/O and ultra-high I/O types. For more information, see `Disk Types and Performance <https://docs.otc.t-systems.com/en-us/usermanual/evs/en-us_topic_0014580744.html>`__.

      Each broker of a 3.x instance can only have 100 GB storage space (not changeable).

   f. **Disk Encryption**: Specify whether to enable disk encryption.

      Enabling disk encryption improves data security, but slows down disk read/write. Disk encryption depends on Key Management Service (KMS). If you enable disk encryption, select a KMS key. **This parameter cannot be modified once the Kafka instance is created.**

   g. **Capacity Threshold Policy**: Policy used when the disk usage reaches the threshold. The capacity threshold is 95%.

      -  **Automatically delete**: Messages can be created and retrieved, but 10% of the earliest messages will be deleted to ensure sufficient disk space. This policy is suitable for scenarios where no service interruption can be tolerated. Data may be lost.
      -  **Stop production**: New messages cannot be created, but existing messages can still be retrieved. This policy is suitable for scenarios where no data loss can be tolerated.

   **If you select Single-node, a v2.7 instance with one broker will be created.**

   a. **Version**: Kafka version, which can only be 2.7.

   b. **CPU Architecture**: The x86 architecture is supported.

   c. **Broker Flavor**: Select a broker flavor that best fit your needs.

   d. **Brokers**: The instance can have only one broker.

   e. **Storage space per broker**: Disk type and size for storing the instance data.

      **The disk type cannot be changed once the Kafka instance is created.**

      The storage space is consumed by message replicas, logs, and metadata. Specify the storage space based on the expected service message size, the number of replicas, and the reserved disk space. Each Kafka broker reserves 33 GB disk space for storing logs and metadata.

      Disks are formatted when an instance is created. As a result, the actual available disk space is 93% to 95% of the total disk space.

      The disk supports high I/O and ultra-high I/O types. For more information, see `Disk Types and Performance <https://docs.otc.t-systems.com/en-us/usermanual/evs/en-us_topic_0014580744.html>`__.

   f. **Disk Encryption**: Specify whether to enable disk encryption.

      Enabling disk encryption improves data security, but slows down disk read/write. Disk encryption depends on Key Management Service (KMS). If you enable disk encryption, select a KMS key. **This parameter cannot be modified once the Kafka instance is created.**

   g. **Capacity Threshold Policy**: Policy used when the disk usage reaches the threshold. The capacity threshold is 95%.

      -  **Automatically delete**: Messages can be created and retrieved, but 10% of the earliest messages will be deleted to ensure sufficient disk space. This policy is suitable for scenarios where no service interruption can be tolerated. Data may be lost.
      -  **Stop production**: New messages cannot be created, but existing messages can still be retrieved. This policy is suitable for scenarios where no data loss can be tolerated.


   .. figure:: /_static/images/en-us_image_0000001756349630.png
      :alt: **Figure 1** Single-node instances

      **Figure 1** Single-node instances

#. Configure the instance network parameters.

   -  Select the created VPC and subnet from the **VPC** drop-down list.

      A VPC provides an isolated virtual network for your Kafka instances. You can configure and manage the network as required.

      .. note::

         After the Kafka instance is created, its VPC and subnet cannot be changed.

   -  Select a security group.

      A security group is a set of rules for accessing a Kafka instance. You can click **Manage Security Group** to view or create security groups on the network console.

      Before accessing a Kafka instance on the client, configure security group rules based on the access mode. For details about security group rules, see :ref:`Table 2 <kafka-ug-180604012__table161395381402>`.

#. Configure the instance access mode.

   .. table:: **Table 2** Instance access modes

      +---------------------------+-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Public or Private Network | Plaintext or Ciphertext | Description                                                                                                                                                                                     |
      +===========================+=========================+=================================================================================================================================================================================================+
      | Private Network Access    | Plaintext Access        | Clients connect to the Kafka instance without SASL authentication.                                                                                                                              |
      |                           |                         |                                                                                                                                                                                                 |
      |                           |                         | Once enabled, private network access cannot be disabled. Enable plaintext or ciphertext access, or both.                                                                                        |
      +---------------------------+-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                           | Ciphertext Access       | Clients connect to the Kafka instance with SASL authentication.                                                                                                                                 |
      |                           |                         |                                                                                                                                                                                                 |
      |                           |                         | Once enabled, private network access cannot be disabled. Enable plaintext or ciphertext access, or both. **To disable ciphertext access, contact customer service.**                            |
      |                           |                         |                                                                                                                                                                                                 |
      |                           |                         | If you enable **Ciphertext Access**, specify a :ref:`security protocol, SASL/PLAIN, username, and password <kafka-ug-180604013__table1914417312419>`.                                           |
      |                           |                         |                                                                                                                                                                                                 |
      |                           |                         | After an instance is created, disabling and re-enabling **Ciphertext Access** do not affect users.                                                                                              |
      +---------------------------+-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Public Network Access     | Plaintext Access        | Clients connect to the Kafka instance without SASL authentication.                                                                                                                              |
      |                           |                         |                                                                                                                                                                                                 |
      |                           |                         | Enable or disable plaintext access, and configure addresses for public network access.                                                                                                          |
      +---------------------------+-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                           | Ciphertext Access       | Clients connect to the Kafka instance with SASL authentication.                                                                                                                                 |
      |                           |                         |                                                                                                                                                                                                 |
      |                           |                         | Enable or disable ciphertext access, and configure addresses for public network access.                                                                                                         |
      |                           |                         |                                                                                                                                                                                                 |
      |                           |                         | If you enable **Ciphertext Access**, specify a :ref:`security protocol, SASL/PLAIN, username, and password <kafka-ug-180604013__table1914417312419>`.                                           |
      |                           |                         |                                                                                                                                                                                                 |
      |                           |                         | After an instance is created, disabling and re-enabling **Ciphertext Access** do not affect users.                                                                                              |
      +---------------------------+-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                           | Public IP Addresses     | Select the number of public IP addresses as required.                                                                                                                                           |
      |                           |                         |                                                                                                                                                                                                 |
      |                           |                         | If EIPs are insufficient, click **Create Elastic IP** to create EIPs. Then, return to the Kafka console and click |image2| next to **Public IP Address** to refresh the public IP address list. |
      |                           |                         |                                                                                                                                                                                                 |
      |                           |                         | **Kafka instances only support IPv4 EIPs.**                                                                                                                                                     |
      +---------------------------+-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      Ciphertext access is unavailable for single-node instances.

   The security protocol, SASL/PLAIN mechanism, username, and password are described as follows.

   .. _kafka-ug-180604013__table1914417312419:

   .. table:: **Table 3** Ciphertext access parameters

      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter             | Value                 | Description                                                                                                                                                                                                               |
      +=======================+=======================+===========================================================================================================================================================================================================================+
      | Security Protocol     | SASL_SSL              | SASL is used for authentication. Data is encrypted with SSL certificates for high-security transmission.                                                                                                                  |
      |                       |                       |                                                                                                                                                                                                                           |
      |                       |                       | SCRAM-SHA-512 is enabled by default. To use PLAIN, enable **SASL/PLAIN**.                                                                                                                                                 |
      |                       |                       |                                                                                                                                                                                                                           |
      |                       |                       | **What are SCRAM-SHA-512 and PLAIN mechanisms?**                                                                                                                                                                          |
      |                       |                       |                                                                                                                                                                                                                           |
      |                       |                       | -  SCRAM-SHA-512: uses the hash algorithm to generate credentials for usernames and passwords to verify identities. SCRAM-SHA-512 is more secure than PLAIN.                                                              |
      |                       |                       | -  PLAIN: a simple username and password verification mechanism.                                                                                                                                                          |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | SASL_PLAINTEXT        | SASL is used for authentication. Data is transmitted in plaintext for high performance.                                                                                                                                   |
      |                       |                       |                                                                                                                                                                                                                           |
      |                       |                       | SCRAM-SHA-512 is enabled by default. To use PLAIN, enable **SASL/PLAIN**. SCRAM-SHA-512 authentication is recommended for plaintext transmission.                                                                         |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | SASL/PLAIN            | ``-``                 | -  If **SASL/PLAIN** is disabled, the SCRAM-SHA-512 mechanism is used for username and password authentication.                                                                                                           |
      |                       |                       | -  If **SASL/PLAIN** is enabled, both the SCRAM-SHA-512 and PLAIN mechanisms are supported. You can select either of them as required.                                                                                    |
      |                       |                       |                                                                                                                                                                                                                           |
      |                       |                       | The **SASL/PLAIN** setting cannot be changed once ciphertext access is enabled.                                                                                                                                           |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Username and Password | ``-``                 | Username and password used by the client to connect to the Kafka instance.                                                                                                                                                |
      |                       |                       |                                                                                                                                                                                                                           |
      |                       |                       | A username should contain 4 to 64 characters, start with a letter, and contain only letters, digits, hyphens (-), and underscores (_).                                                                                    |
      |                       |                       |                                                                                                                                                                                                                           |
      |                       |                       | A password must meet the following requirements:                                                                                                                                                                          |
      |                       |                       |                                                                                                                                                                                                                           |
      |                       |                       | -  Contains 8 to 32 characters.                                                                                                                                                                                           |
      |                       |                       | -  Contains at least three types of the following characters: uppercase letters, lowercase letters, digits, and special characters \`~! @#$ ``%^&*()-_=+\|[{}];:'",<.>?`` and spaces, and cannot start with a hyphen (-). |
      |                       |                       | -  Cannot be the username spelled forwards or backwards.                                                                                                                                                                  |
      |                       |                       |                                                                                                                                                                                                                           |
      |                       |                       | The username cannot be changed once ciphertext access is enabled.                                                                                                                                                         |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Advanced Settings** to configure more parameters.

   a. Configure **Automatic Topic Creation**.

      This setting is disabled by default. You can enable or disable it as required.

      If this option is enabled, a topic will be automatically created when a message is produced in or consumed from a topic that does not exist. By default, the topic has parameters listed in :ref:`Table 4 <kafka-ug-180604013__table46677586328>`.

      After you change the value of the **log.retention.hours**, **default.replication.factor**, or **num.partitions** parameter, the value will be used in later topics that are automatically created. For example, assume that **num.partitions** is changed to 5, an automatically created topic has parameters listed in :ref:`Table 4 <kafka-ug-180604013__table46677586328>`.

      .. _kafka-ug-180604013__table46677586328:

      .. table:: **Table 4** Topic parameters

         ========================= ============= ==============
         Parameter                 Default Value Modified Value
         ========================= ============= ==============
         Partitions                3             5
         Replicas                  3             3
         Aging Time (h)            72            72
         Synchronous Replication   Disabled      Disabled
         Synchronous Flushing      Disabled      Disabled
         Message Timestamp         CreateTime    CreateTime
         Max. Message Size (bytes) 10,485,760    10,485,760
         ========================= ============= ==============

   b. Specify **Tags**.

      Tags are used to identify cloud resources. When you have multiple cloud resources of the same type, you can use tags to classify them based on usage, owner, or environment.

      -  If you have predefined tags, select a predefined pair of tag key and value. You can click **View predefined tags** to go to the Tag Management Service (TMS) console and view or create tags.
      -  You can also create new tags by specifying **Tag key** and **Tag value**.

      Up to 20 tags can be added to each Kafka instance. For details about the requirements on tags, see :ref:`Configuring Kafka Instance Tags <tagmanagement>`.

   c. Enter a **Description** of the instance for 0-1024 characters.

#. Click **Create**.

#. Confirm the instance information, and click **Submit**.

#. Return to the instance list and check whether the Kafka instance has been created.

   It takes 3 to 15 minutes to create an instance. During this period, the instance status is **Creating**.

   -  If the instance is created successfully, its status changes to **Running**.
   -  If the instance is in the **Creation failed** state, delete it by referring to :ref:`Deleting Kafka Instances <kafka-ug-180604016>`. Then create a new one. If the instance creation fails again, contact customer service.

      .. note::

         Instances that fail to be created do not occupy other resources.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0000001707049736.png
