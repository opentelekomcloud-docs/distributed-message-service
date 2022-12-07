:original_name: kafka-ug-180801001.html

.. _kafka-ug-180801001:

Accessing a Kafka Instance with SASL
====================================

If you enable SASL_SSL when creating an instance, data will be encrypted before transmission for enhanced security.

For security purposes, **TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256** is supported.

This section describes how to use an open-source Kafka client to access a Kafka instance if SASL has been enabled for the instance. There are two scenarios. For cross-VPC access, see :ref:`Cross-VPC Access to a Kafka Instance <kafka-ug-0001>`. For DNAT-based access, see :ref:`Using DNAT to Access a Kafka Instance <kafka-dnat>`.

.. note::

   Each Kafka broker allows a maximum of 1000 connections from each IP address by default. Excess connections will be rejected. You can change the limit by referring to :ref:`Modifying Kafka Parameters <kafka-ug-0007>`.

Prerequisites
-------------

-  Security group rules have been correctly configured.

   A Kafka instance with SASL enabled can be accessed **within a VPC** or **over public networks**. Ensure that security group rules have been correctly configured for the instance. For details about security group configuration requirements, see :ref:`Table 2 <kafka-ug-180604012__table161395381402>`.

-  .. _kafka-ug-180801001__li10340528173815:

   The instance connection address has been obtained.

   -  For intra-VPC access, use port 9093. Obtain the instance connection address in the **Connection** section of the **Basic Information** tab page.


      .. figure:: /_static/images/en-us_image_0000001328644244.png
         :alt: **Figure 1** Kafka instance connection addresses for intra-VPC access with SASL

         **Figure 1** Kafka instance connection addresses for intra-VPC access with SASL

   -  For public access, use port 9095. Obtain the instance connection address in the **Connection** section of the **Basic Information** tab page.


      .. figure:: /_static/images/en-us_image_0000001379445357.png
         :alt: **Figure 2** Kafka instance connection addresses for public access with SASL

         **Figure 2** Kafka instance connection addresses for public access with SASL

-  If automatic topic creation is not enabled for the Kafka instance, :ref:`create a topic <dms-ug-180604018>` before connecting to the instance.

-  The **client.truststore.jks** certificate has been downloaded. Click the Kafka instance to go to the **Basic Information** tab page. Click **Download** next to **SSL Certificate** in the **Connection** area. Download and decompress the package to obtain the client certificate file **client.truststore.jks**.

-  Kafka CLI `v1.1.0 <https://archive.apache.org/dist/kafka/1.1.0/kafka_2.11-1.1.0.tgz>`__, `v2.7.2 <https://archive.apache.org/dist/kafka/2.7.2/kafka_2.12-2.7.2.tgz>`__, or `v2.3.0 <https://archive.apache.org/dist/kafka/2.3.0/kafka_2.11-2.3.0.tgz>`__ is available. Ensure that the Kafka instance and the CLI are of the same version.

-  An ECS has been created. For intra-VPC access, ensure that its VPC, subnet, and security group configurations are the same as those of the Kafka instance. `JDK v1.8.111 or later <https://www.oracle.com/java/technologies/downloads/#java8>`__ has been installed on the ECS, and the **JAVA_HOME** and **PATH** environment variables have been configured as follows:

   Add the following lines to the **.bash_profile** file in the home directory as an authorized user: In this command, **/opt/java/jdk1.8.0_151** is the JDK installation path. Change it to the path where you install JDK.

   .. code-block::

      export JAVA_HOME=/opt/java/jdk1.8.0_151
      export PATH=$JAVA_HOME/bin:$PATH

   Run the **source .bash_profile** command for the modification to take effect.

Accessing the Instance Using CLI
--------------------------------

The following uses Linux as an example.

#. Map hosts to IP addresses in the **/etc/hosts** file on the host where the client is located, so that the client can quickly parse the instance brokers.

   Set IP addresses to the instance connection addresses obtained in :ref:`Prerequisites <kafka-ug-180801001__li10340528173815>`. Set hosts to the names of instance hosts. Specify a unique name for each host.

   For example:

   10.154.48.120 server01

   10.154.48.121 server02

   10.154.48.122 server03

#. Decompress the Kafka CLI package.

   Access the directory where the CLI package is stored and run the following command to decompress the package:

   **tar -zxf [kafka_tar]**

   In the preceding command, *[kafka_tar]* indicates the name of the CLI package.

   For example:

   **tar -zxf kafka_2.12-2.7.2.tgz**

#. .. _kafka-ug-180801001__li5414277457:

   Modify the configuration file of the Kafka CLI.

   Find the **consumer.properties** and **producer.properties** files in the **/config** directory of the Kafka CLI and add the following content to the files:

   .. code-block::

      sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required \
      username="**********" \
      password="**********";
      sasl.mechanism=PLAIN

      security.protocol=SASL_SSL
      ssl.truststore.location={ssl_truststore_path}
      ssl.truststore.password=dms@kafka
      ssl.endpoint.identification.algorithm=

   Parameter description:

   -  **username** and **password**: username and password you set when enabling SASL_SSL during Kafka instance creation or when creating a SASL_SSL user.
   -  **ssl.truststore.location**: path for storing the **client.truststore.jks** certificate. Even in Windows, you need to use slashes (/) for the certificate path. Do not use backslashes (\\), which are used by default for paths in Windows. Otherwise, the client will fail to obtain the certificate.
   -  **ssl.truststore.password**: server certificate password, which must be set to **dms@kafka** and cannot be changed.
   -  **ssl.endpoint.identification.algorithm**: whether to verify the certificate domain name. **This parameter must be left blank, which indicates disabling domain name verification**.

#. Access the **/bin** directory of the Kafka CLI.

   In Windows, you need to access the **/bin/windows** directory.

#. Run the following command to create messages:

   .. code-block::

      ./kafka-console-producer.sh --broker-list ${connection-address} --topic ${topic-name} --producer.config ../config/producer.properties

   Parameter description:

   -  *{connection-address}*: the address obtained in :ref:`Prerequisites <kafka-ug-180801001__li10340528173815>`. For public access, use **Instance Address (Public Network)**. For intra-VPC access, use **Instance Address (Private Network)**.
   -  *{topic-name}*: the name of the topic created for the Kafka instance If automatic topic creation has enabled for the Kafka instance, set this parameter to the name of a created topic or a topic that has not been created.

   The following example uses connection addresses **10.3.196.45:9095,10.78.42.127:9095,10.4.49.103:9095**.

   After running the preceding command, you can send a message to the Kafka instance by writing it and pressing **Enter**. Each line of content is sent as a message.

   .. code-block:: console

      [root@ecs-kafka bin]#./kafka-console-producer.sh --broker-list 10.3.196.45:9095,10.78.42.127:9095,10.4.49.103:9095  --topic topic-demo --producer.config ../config/producer.properties
      >Hello
      >DMS
      >Kafka!
      >^C[root@ecs-kafka bin]#

   To stop creating messages, press **Ctrl**\ +\ **C** to exit.

#. Run the following command to retrieve messages:

   .. code-block::

      ./kafka-console-consumer.sh --bootstrap-server ${connection-address} --topic ${topic-name} --group ${consumer-group-name} --from-beginning  --consumer.config ../config/consumer.properties

   Parameter description:

   -  *{connection-address}*: the address obtained in :ref:`Prerequisites <kafka-ug-180801001__li10340528173815>`. For public access, use **Instance Address (Public Network)**. For intra-VPC access, use **Instance Address (Private Network)**.
   -  *{topic-name}*: the name of the topic created for the Kafka instance
   -  *{consumer-group-name}*: the consumer group name set based on your service requirements. **If a consumer group name has been specified in the configuration file, ensure that you use the same name in the command line. Otherwise, consumption may fail.** If a consumer group name starts with a special character, such as an underscore (_) or a number sign (#), the monitoring data cannot be displayed.

   Example:

   .. code-block:: console

      [root@ecs-kafka bin]#  ./kafka-console-consumer.sh --bootstrap-server 10.3.196.45:9095,10.78.42.127:9095,10.4.49.103:9095 --topic topic-demo --group order-test --from-beginning --consumer.config ../config/consumer.properties
      Hello
      DMS
      Kafka!
      ^CProcessed a total of 3 messages
      [root@ecs-kafka bin]#

   To stop retrieving messages, press **Ctrl**\ +\ **C** to exit.
