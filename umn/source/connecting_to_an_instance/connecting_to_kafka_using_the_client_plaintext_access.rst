:original_name: kafka-ug-180604020.html

.. _kafka-ug-180604020:

Connecting to Kafka Using the Client (Plaintext Access)
=======================================================

This section describes how to use an open-source Kafka client to access a Kafka instance in plaintext. Two scenarios: private network within a VPC and public network. To access a Kafka instance across VPCs, see :ref:`Accessing Kafka Using a VPC Endpoint Across VPCs <kafka-ug-0001>`. To access a Kafka instance using DNAT, see :ref:`Accessing Kafka in a Public Network Using DNAT <kafka-dnat>`. To access an instance in your service code, see the `Distributed Message Service Developer Guide <https://docs.otc.t-systems.com/en-us/devg/dms/Kafka-summary.html>`__.

For details on how to use a Kafka client in different languages, visit https://cwiki.apache.org/confluence/display/KAFKA/Clients.

.. note::

   Each Kafka broker allows a maximum of 1000 connections from each IP address. Excess connections will be rejected. You can change the limit by referring to :ref:`Modifying Kafka Instance Configuration Parameters <kafka-ug-0007>`, that is, to modify parameter **max.connections.per.ip**.

Prerequisites
-------------

-  Security group rules have been properly configured.

   To access a Kafka instance with ciphertext access disabled, configure proper security group rules. For details about security group configuration requirements, see :ref:`Table 2 <kafka-ug-180604012__table161395381402>`.

-  .. _kafka-ug-180604020__li139061643115913:

   The Kafka instance address has been obtained.

   -  To access a Kafka instance in a private network within a VPC, use port 9092. Obtain the instance connection address in the **Connection** section of the **Basic Information** page, shown as follows.


      .. figure:: /_static/images/en-us_image_0000001756356494.png
         :alt: **Figure 1** Kafka instance addresses for private access within a VPC (in plaintext)

         **Figure 1** Kafka instance addresses for private access within a VPC (in plaintext)

   -  To access a Kafka instance in a public network, use port 9094. Obtain the instance connection address in the **Connection** section of the **Basic Information** page, shown as follows.


      .. figure:: /_static/images/en-us_image_0000001756206030.png
         :alt: **Figure 2** Kafka instance addresses for public access (in plaintext)

         **Figure 2** Kafka instance addresses for public access (in plaintext)

-  If automatic topic creation is not enabled for the Kafka instance, :ref:`create a topic <kafka-ug-180604018>` before connecting to the instance.

-  Kafka CLI `v1.1.0 <https://archive.apache.org/dist/kafka/1.1.0/kafka_2.11-1.1.0.tgz>`__, `v2.3.0 <https://archive.apache.org/dist/kafka/2.3.0/kafka_2.11-2.3.0.tgz>`__, `v2.7.2 <https://archive.apache.org/dist/kafka/2.7.2/kafka_2.12-2.7.2.tgz>`__, or `v3.4.0 <https://archive.apache.org/dist/kafka/3.4.0/kafka_2.12-3.4.0.tgz>`__ is available. Ensure that the Kafka instance and the CLI use the same version.

-  An ECS that has an EIP has been created. For intra-VPC access, ensure that its VPC, subnet, and security group configurations are the same as those of the Kafka instance. `JDK v1.8.111 or later <https://www.oracle.com/java/technologies/downloads/#java8>`__ has been installed on the ECS, and the **JAVA_HOME** and **PATH** environment variables have been configured as follows:

   Add the following lines to the **.bash_profile** file in the home directory as an authorized user. In this command, **/opt/java/jdk1.8.0_151** is the JDK installation path. Change it to the path where you install JDK.

   .. code-block::

      export JAVA_HOME=/opt/java/jdk1.8.0_151
      export PATH=$JAVA_HOME/bin:$PATH

   Run the **source .bash_profile** command for the modification to take effect.

Accessing the Instance Using CLI
--------------------------------

The following uses Linux as an example.

#. Decompress the Kafka CLI package.

   Access the directory where the CLI package is stored and run the following command to decompress the package:

   **tar -zxf [kafka_tar]**

   In the preceding command, *[kafka_tar]* indicates the name of the CLI package.

   For example:

   **tar -zxf kafka_2.12-2.7.2.tgz**

#. Access the **/bin** directory of the Kafka CLI.

   In Windows, you need to access the **/bin/windows** directory.

#. Run the following command to create messages:

   .. code-block::

      ./kafka-console-producer.sh --broker-list ${connection-address} --topic ${topic-name}

   Parameter description:

   -  *{connection-address}*: the address obtained in :ref:`Prerequisites <kafka-ug-180604020__li139061643115913>`. For public access, use **Address (Public Network, Plaintext)**. For intra-VPC access, use **Address (Private Network, Plaintext)**.
   -  *{topic-name}*: the name of the topic created for the Kafka instance. If automatic topic creation has enabled for the Kafka instance, set this parameter to the name of a created topic or a topic that has not been created.

   The following example uses connection addresses **10.xx.xx.45:9094,10.xx.xx.127:9094,10.xx.xx.103:9094**. After running the preceding command, you can send a message to the Kafka instance by writing it and pressing **Enter**. Each line of content is sent as a message.

   .. code-block:: console

      [root@ecs-kafka bin]# ./kafka-console-producer.sh --broker-list 10.xx.xx.45:9094,10.xx.xx.127:9094,10.xx.xx.103:9094  --topic topic-demo
      >Hello
      >DMS
      >Kafka!
      >^C[root@ecs-kafka bin]#

   To stop creating messages, press **Ctrl**\ +\ **C** to exit.

#. Run the following command to retrieve messages:

   .. code-block::

      ./kafka-console-consumer.sh --bootstrap-server ${connection-address} --topic ${topic-name} --group ${consumer-group-name} --from-beginning

   Parameter description:

   -  *{connection-address}*: the address obtained in :ref:`Prerequisites <kafka-ug-180604020__li139061643115913>`. For public access, use **Address (Public Network, Plaintext)**. For intra-VPC access, use **Address (Private Network, Plaintext)**.
   -  *{topic-name}*: the name of the topic created for the Kafka instance
   -  *{consumer-group-name}*: the consumer group name set based on your service requirements. **If a consumer group name has been specified in the configuration file, ensure that you use the same name in the command line. Otherwise, consumption may fail.** If a consumer group name starts with a special character, such as an underscore (_) or a number sign (#), the monitoring data cannot be displayed.

   Example:

   .. code-block:: console

      [root@ecs-kafka bin]#  ./kafka-console-consumer.sh --bootstrap-server 10.xx.xx.45:9094,10.xx.xx.127:9094,10.xx.xx.103:9094 --topic topic-demo --group order-test --from-beginning
      Kafka!
      DMS
      Hello
      ^CProcessed a total of 3 messages
      [root@ecs-kafka bin]#

   To stop retrieving messages, press **Ctrl**\ +\ **C** to exit.
