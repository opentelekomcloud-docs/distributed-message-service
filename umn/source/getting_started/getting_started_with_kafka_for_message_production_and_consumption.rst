:original_name: kafka-qs-0409001.html

.. _kafka-qs-0409001:

Getting Started with Kafka for Message Production and Consumption
=================================================================

This section takes the example of creating a Kafka instance (ciphertext access and SASL_SSL) and accessing it on the client (private network, within a virtual private cloud (VPC)) for message production and consumption to get you quickly started with Distributed Message Service (DMS).


.. figure:: /_static/images/en-us_image_0000001927807598.png
   :alt: **Figure 1** Procedure for using DMS for Kafka

   **Figure 1** Procedure for using DMS for Kafka

#. :ref:`Step 1: Preparations <kafka-qs-0409001__section729541193917>`

   A Kafka instance runs in a VPC. Before creating a Kafka instance, ensure that a VPC is available.

   After a Kafka instance is created, download and install the Kafka open-source client on your ECS before producing and consuming messages.

#. :ref:`Step 2: Create a Kafka Instance <kafka-qs-0409001__section1955221261010>`

   You can select the specification and quantity, and enable ciphertext access and SASL_SSL when creating a Kafka instance.

   When connecting to a Kafka instance with SASL_SSL enabled, SASL is used for authentication. Data is encrypted with SSL certificates for high-security transmission.

#. :ref:`Step 3: Create a Topic <kafka-qs-0409001__section1794732717149>`

   Topics store messages created by producers and subscribed by consumers.

   This section uses the example of creating a topic on the console.

#. :ref:`Step 4: Connect to a Kafka Instance to Produce and Consume Messages <kafka-qs-0409001__section15618113310177>`

   Before connecting to a Kafka instance with SASL_SSL enabled, download the certificate and configure the connection in the client configuration file.

.. _kafka-qs-0409001__section729541193917:

Step 1: Preparations
--------------------

#. Grant Kafka instance permissions.

   To achieve fine-grained management of your cloud resources, create Identity and Access Management (IAM) user groups and users and grant specified permissions to the users. For more information, see :ref:`Creating a User and Granting DMS for Kafka Permissions <createuserandgrantpolicy>`.

#. .. _kafka-qs-0409001__li79912171816:

   Create a VPC and subnet.

   Before creating a Kafka instance, ensure that a VPC and a subnet are available. For details about how to create a VPC and a subnet, see `Creating a VPC <https://docs.otc.t-systems.com/en-us/usermanual/vpc/en-us_topic_0013935842.html>`__.

   .. important::

      The VPC must be created in the same region as the Kafka instance.

#. .. _kafka-qs-0409001__li15466154716411:

   Create a security group and add security group rules.

   Before creating a Kafka instance, ensure that a security group is available. For details about how to create a security group, see `Creating a Security Group <https://docs.otc.t-systems.com/en-us/usermanual/vpc/en-us_topic_0013748715.html>`__.

   To connect to Kafka instances, add the security group rules described in :ref:`Table 1 <kafka-qs-0409001__table161395381402>`. Other rules can be added based on site requirements.

   .. _kafka-qs-0409001__table161395381402:

   .. table:: **Table 1** Security group rules

      +-----------+----------+------+----------------+--------------------------------------------------------------------------------+
      | Direction | Protocol | Port | Source address | Description                                                                    |
      +===========+==========+======+================+================================================================================+
      | Inbound   | TCP      | 9093 | 0.0.0.0/0      | Accessing a Kafka instance over a private network within a VPC (in ciphertext) |
      +-----------+----------+------+----------------+--------------------------------------------------------------------------------+

   .. note::

      After a security group is created, it has a default inbound rule that allows communication among ECSs within the security group and a default outbound rule that allows all outbound traffic. If you access your Kafka instance using the private network within a VPC, you do not need to add the rules described in :ref:`Table 1 <kafka-qs-0409001__table161395381402>`.

#. Construct a client for message production and consumption.

   This section uses a Linux elastic cloud server (ECS) as the client. Before creating a Kafka instance, create an ECS with an EIP, install the JDK, configure environment variables, and download an open-source Kafka client.

   a. Log in to the console, click |image1| in the upper left corner, click **Elastic Cloud Server** under **Computing**, and then create an ECS.

      For details about how to create an ECS, see `Creating an ECS <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0021831611.html>`__. If you already have an available ECS, skip this step.

   b. Log in to an ECS as user **root**.

   c. Install Java JDK and configure the environment variables **JAVA_HOME** and **PATH**.

      #. Download a JDK.

         .. note::

            Use Oracle JDK instead of ECS's default JDK (for example, OpenJDK), because ECS's default JDK may not be suitable. Obtain Oracle JDK 1.8.111 or later from `Oracle's official website <https://www.oracle.com/java/technologies/downloads/#java8>`__.

      #. Decompress the JDK.

         .. code-block::

            tar -zxvf jdk-8u321-linux-x64.tar.gz

         Change **jdk-8u321-linux-x64.tar.gz** to your JDK version.

      #. Open the **.bash_profile** file.

         .. code-block::

            vim ~/.bash_profile

      #. Add the following content:

         .. code-block::

            export JAVA_HOME=/root/jdk1.8.0_321
            export PATH=$JAVA_HOME/bin:$PATH

         Change **/root/jdk1.8.0_321** to the path where you install JDK.

      #. Press **Esc**. Enter the following line and press **Enter**. Save the **.bash_profile** file and exit.

         .. code-block::

            :wq

      #. Run the following command to make the change take effect:

         .. code-block::

            source .bash_profile

      #. Check whether the JDK is installed.

         .. code-block::

            java -version

         If the following message is returned, the JDK is installed.

         .. code-block::

            java version "1.8.0_321"

   d. Download an open-source Kafka client.

      .. code-block::

         wget https://archive.apache.org/dist/kafka/2.7.2/kafka_2.12-2.7.2.tgz

   e. Run the following command to decompress the package:

      .. code-block::

         tar -zxf kafka_2.12-2.7.2.tgz

.. _kafka-qs-0409001__section1955221261010:

Step 2: Create a Kafka Instance
-------------------------------

#. Log in to the DMS console, then click **Create Instance** in the upper right corner of the page.

#. Set basic instance information. :ref:`Table 2 <kafka-qs-0409001__table035715811538>` lists the configuration details.

   .. _kafka-qs-0409001__table035715811538:

   .. table:: **Table 2** Basic instance settings

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                   |
      +===================================+===============================================================================================================================================================================================================================================================================================================+
      | Region                            | DMS for Kafka in different regions cannot communicate with each other over an intranet. Select a nearest location for low latency and fast access.                                                                                                                                                            |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   | Select eu-de.                                                                                                                                                                                                                                                                                                 |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Project                           | Projects isolate compute, storage, and network resources across geographical regions. For each region, a preset project is available.                                                                                                                                                                         |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   | Select eu-de (default).                                                                                                                                                                                                                                                                                       |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | AZ                                | An AZ is a physical region where resources use independent power supply and networks. AZs are physically isolated but interconnected through an internal network.                                                                                                                                             |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   | Select **AZ1**, **AZ2**, and **AZ3**.                                                                                                                                                                                                                                                                         |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Instance Name                     | You can customize a name that complies with the rules: 4-64 characters; starts with a letter; can contain only letters, digits, hyphens (-), and underscores (_).                                                                                                                                             |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   | Enter **kafka-test**.                                                                                                                                                                                                                                                                                         |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Enterprise Project                | This parameter is for enterprise users. An enterprise project manages project resources in groups. Enterprise projects are logically isolated.                                                                                                                                                                |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   | Select **default**.                                                                                                                                                                                                                                                                                           |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Specifications                    | Select **Cluster** to create a cluster Kafka instance.                                                                                                                                                                                                                                                        |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Version                           | Kafka version. Cannot be changed once the instance is created.                                                                                                                                                                                                                                                |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   | Select **2.7**.                                                                                                                                                                                                                                                                                               |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | CPU Architecture                  | **x86**                                                                                                                                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   | Retain the default value.                                                                                                                                                                                                                                                                                     |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Broker Flavor                     | Select a broker flavor as required.                                                                                                                                                                                                                                                                           |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   | Select **kafka.2u4g.cluster**.                                                                                                                                                                                                                                                                                |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Brokers                           | Specify the number of brokers as required.                                                                                                                                                                                                                                                                    |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   | Enter **3**.                                                                                                                                                                                                                                                                                                  |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Storage Space per Broker          | Select the disk type and specify the disk size as required.                                                                                                                                                                                                                                                   |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   | Total storage space = Storage space per broker x Broker quantity. After the instance is created, you cannot change the disk type.                                                                                                                                                                             |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   | Select **Ultra-high I/O** and enter **100**.                                                                                                                                                                                                                                                                  |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Disk Encryption                   | Skip it.                                                                                                                                                                                                                                                                                                      |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Capacity Threshold Policy         | Select **Automatically delete**: When the disk reaches the disk capacity threshold (95%), messages can still be produced and consumed, but the earliest 10% of messages will be deleted to ensure sufficient disk space. Use this policy for services intolerant of interruptions. However, data may be lost. |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Configure the instance network. For details, see :ref:`Table 3 <kafka-qs-0409001__table1315151192117>`.

   .. _kafka-qs-0409001__table1315151192117:

   .. table:: **Table 3** Configuring instance network

      +-----------------------------------+--------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                          |
      +===================================+======================================================================================+
      | VPC                               | The VPC and subnet cannot be changed once the instance is created.                   |
      |                                   |                                                                                      |
      |                                   | Select the VPC and subnet prepared in :ref:`2 <kafka-qs-0409001__li79912171816>`.    |
      +-----------------------------------+--------------------------------------------------------------------------------------+
      | Security Group                    | Select the security group prepared in :ref:`3 <kafka-qs-0409001__li15466154716411>`. |
      +-----------------------------------+--------------------------------------------------------------------------------------+

#. Set the instance access mode. For details, see :ref:`Table 4 <kafka-qs-0409001__table20282145310365>`.

   .. _kafka-qs-0409001__table20282145310365:

   .. table:: **Table 4** Setting the instance access mode

      +------------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter              | Sub-Parameter         | Description                                                                                                                                                                                                                   |
      +========================+=======================+===============================================================================================================================================================================================================================+
      | Private Network Access | Plaintext Access      | Disable it.                                                                                                                                                                                                                   |
      +------------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                        | Ciphertext Access     | When this parameter is enabled, SASL authentication is required when a client connects to the Kafka instance.                                                                                                                 |
      |                        |                       |                                                                                                                                                                                                                               |
      |                        |                       | a. **Ciphertext Access** is enabled.                                                                                                                                                                                          |
      |                        |                       |                                                                                                                                                                                                                               |
      |                        |                       | b. **SASL_SSL** is selected. **Username** and **Password** can be set. Enter "test" for the username. The username cannot be changed once ciphertext access is enabled.                                                       |
      |                        |                       |                                                                                                                                                                                                                               |
      |                        |                       |    A username should contain 4 to 64 characters, start with a letter, and contain only letters, digits, hyphens (-), and underscores (_).                                                                                     |
      |                        |                       |                                                                                                                                                                                                                               |
      |                        |                       |    A password must meet the following requirements:                                                                                                                                                                           |
      |                        |                       |                                                                                                                                                                                                                               |
      |                        |                       |    -  Contains 8 to 32 characters.                                                                                                                                                                                            |
      |                        |                       |    -  Contains at least three types of the following characters: uppercase letters, lowercase letters, digits, and special characters \`~! @#$\ ``%^&*()-_=+\|[{}];:'",<.>?`` and spaces, and cannot start with a hyphen (-). |
      |                        |                       |    -  Cannot be the username spelled forwards or backwards.                                                                                                                                                                   |
      |                        |                       |                                                                                                                                                                                                                               |
      |                        |                       | c. **SASL/PLAIN** is enabled.                                                                                                                                                                                                 |
      +------------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Public Network Access  | ``-``                 | Skip it.                                                                                                                                                                                                                      |
      +------------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Skip **Advanced Settings**.

#. Click **Create**.

#. Confirm the instance settings.

#. Return to the **DMS for Kafka** page and check whether the instance has been created.

   It takes 3 to 15 minutes to create an instance. During this period, the instance status is **Creating**.

   -  If the instance is created successfully, its status changes to **Running**.
   -  If the instance is in the **Creation failed** state, delete it, and create a new one. If the instance creation fails again, contact customer service.

      .. note::

         Instances that fail to be created do not occupy other resources.

#. After the instance is created, click its name to go to the instance details page.

#. .. _kafka-qs-0409001__li1363923115616:

   In the **Connection** area, view and record the connection address.


   .. figure:: /_static/images/en-us_image_0000001987139953.png
      :alt: **Figure 2** Kafka instance addresses (private network) for intra-VPC access

      **Figure 2** Kafka instance addresses (private network) for intra-VPC access

.. _kafka-qs-0409001__section1794732717149:

Step 3: Create a Topic
----------------------

#. On the **DMS for Kafka** page, click a Kafka instance.

#. In the navigation pane, choose **Topics**.

#. Click **Create Topic**.

#. .. _kafka-qs-0409001__li11652913193216:

   Enter the topic name, specify other parameters by referring to :ref:`Table 5 <kafka-qs-0409001__table186364410350>`, and click **OK**.

   .. _kafka-qs-0409001__table186364410350:

   .. table:: **Table 5** Topic parameters

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                          |
      +===================================+======================================================================================================================================================================================================================================+
      | Topic Name                        | Customize a name that contains 3 to 200 characters, starts with a letter or underscore (_), and contains only letters, digits, periods (.), hyphens (-), and underscores (_).                                                        |
      |                                   |                                                                                                                                                                                                                                      |
      |                                   | The name must be different from preset topics:                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                                      |
      |                                   | -  \__consumer_offsets                                                                                                                                                                                                               |
      |                                   | -  \__transaction_state                                                                                                                                                                                                              |
      |                                   | -  \__trace                                                                                                                                                                                                                          |
      |                                   | -  \__connect-status                                                                                                                                                                                                                 |
      |                                   | -  \__connect-configs                                                                                                                                                                                                                |
      |                                   | -  \__connect-offsets                                                                                                                                                                                                                |
      |                                   |                                                                                                                                                                                                                                      |
      |                                   | Cannot be changed once the topic is created.                                                                                                                                                                                         |
      |                                   |                                                                                                                                                                                                                                      |
      |                                   | Enter **topic-01**.                                                                                                                                                                                                                  |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Partitions                        | If the number of partitions is the same as that of consumers, the larger the partitions, the higher the consumption concurrency.                                                                                                     |
      |                                   |                                                                                                                                                                                                                                      |
      |                                   | Enter **3**.                                                                                                                                                                                                                         |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Replicas                          | Data is automatically backed up to each replica. When one Kafka broker becomes faulty, data is still available. A higher number of replicas delivers higher reliability.                                                             |
      |                                   |                                                                                                                                                                                                                                      |
      |                                   | Enter **3**.                                                                                                                                                                                                                         |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Aging Time (h)                    | How long messages will be preserved in the topic. Messages older than this period cannot be consumed. They will be deleted, and can no longer be consumed.                                                                           |
      |                                   |                                                                                                                                                                                                                                      |
      |                                   | Enter **72**.                                                                                                                                                                                                                        |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronous Replication           | Skip it. When this option is disabled, leader replicas are independent from follower replica synchronization. They receive messages and write them to local logs, then immediately send the successfully written ones to the client. |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronous Flushing              | Skip it. When this option is disabled, messages are produced and stored in memory instead of written to the disk immediately.                                                                                                        |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Message Timestamp                 | Select **CreateTime**: time when the producer created the message.                                                                                                                                                                   |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Max. Message Size (bytes)         | Maximum batch processing size allowed by Kafka. If message compression is enabled in the client configuration file or code of producers, this parameter indicates the size after compression.                                        |
      |                                   |                                                                                                                                                                                                                                      |
      |                                   | Enter **10,485,760**.                                                                                                                                                                                                                |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _kafka-qs-0409001__section15618113310177:

Step 4: Connect to a Kafka Instance to Produce and Consume Messages
-------------------------------------------------------------------

#. Prepare the file for production and consumption configuration.

   a. Log in to a Linux ECS.

   b. .. _kafka-qs-0409001__li193810310517:

      Download the **client.jks** certificate and upload it to the **/root** directory on the ECS.

      To obtain the certificate: On the Kafka console, click the Kafka instance to go to the **Basic Information** page. Click **Download** next to **SSL Certificate** in the **Connection** area. Decompress the package to obtain the client certificate file **client.jks**.

      .. note::

         **/root** is the path for storing the certificate. Change it to the actual path if needed.

   c. Go to the **/config** directory on the Kafka client.

      .. code-block::

         cd kafka_2.12-2.7.2/config

   d. Add the following commands in both the **consumer.properties** and **producer.properties** files (PLAIN is used as an example).

      .. code-block::

         sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required \
         username="**********" \
         password="**********";
         sasl.mechanism=PLAIN

         security.protocol=SASL_SSL
         ssl.truststore.location={ssl_truststore_path}
         ssl.truststore.password=dms@kafka
         ssl.endpoint.identification.algorithm=

      Description:

      -  **username** and **password** are specified when enabling ciphertext access during instance creation.
      -  **ssl.truststore.location** is the path for storing the certificate obtained in :ref:`1.b <kafka-qs-0409001__li193810310517>`.
      -  **ssl.truststore.password** is certified by the server, which must be set to **dms@kafka** and cannot be changed.
      -  **ssl.endpoint.identification.algorithm** decides whether to verify the certificate domain name. In this example, **leave this parameter blank, which indicates disabling domain name verification**.

#. Go to the **/bin** directory on the Kafka client.

   .. code-block::

      cd ../bin

#. Produce messages.

   .. code-block::

      ./kafka-console-producer.sh --broker-list ${connection address} --topic ${topic name} --producer.config ../config/producer.properties

   Description:

   -  *{connection address}*: the connection address obtained in :ref:`10 <kafka-qs-0409001__li1363923115616>`
   -  *{topic name}*: the topic name obtained in :ref:`4 <kafka-qs-0409001__li11652913193216>`

   For example, **192.xxx.xxx.xxx:9093**, **192.xxx.xxx.xxx:9093**, **192.xxx.xxx.xxx:9093** are the connection addresses of the Kafka instance.

   After running this command, you can send messages to the Kafka instance by entering the information as prompted and pressing **Enter**. Each line of content will be sent as a message.

   .. code-block:: console

      [root@ecs-kafka bin]#./kafka-console-producer.sh --broker-list 192.xxx.xxx.xxx:9093,192.xxx.xxx.xxx:9093,192.xxx.xxx.xxx:9093  --topic topic-01 --producer.config ../config/producer.properties
      >Hello
      >DMS
      >Kafka!
      >^C[root@ecs-kafka bin]#

   Press **Ctrl+C** to cancel.

#. Consume messages.

   .. code-block::

      ./kafka-console-consumer.sh --bootstrap-server ${connection address} --topic ${topic name} --from-beginning  --consumer.config ../config/consumer.properties

   Description:

   -  *{connection address}*: the connection address obtained in :ref:`10 <kafka-qs-0409001__li1363923115616>`
   -  *{topic name}*: the topic name obtained in :ref:`4 <kafka-qs-0409001__li11652913193216>`

   Sample:

   .. code-block:: console

      [root@ecs-kafka bin]#  ./kafka-console-consumer.sh --bootstrap-server 192.xxx.xxx.xxx:9093,192.xxx.xxx.xxx:9093,192.xxx.xxx.xxx:9093 --topic topic-01 --from-beginning --consumer.config ../config/consumer.properties
      Hello
      Kafka!
      DMS
      ^CProcessed a total of 3 messages
      [root@ecs-kafka bin]#

   Press **Ctrl+C** to cancel.

.. |image1| image:: /_static/images/en-us_image_0000001143589128.png
