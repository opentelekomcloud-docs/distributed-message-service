:original_name: kafka-ug-180801001.html

.. _kafka-ug-180801001:

Connecting to Kafka Using the Client (Ciphertext Access)
========================================================

This section describes how to access a Kafka instance in ciphertext on an open-source Kafka client. The client connects to the Kafka instance with SASL authentication. If the security protocol **SASL_SSL** is used, the client communicates with the Kafka instance in encryption, improving security.

Notes and Constraints
---------------------

-  For security purposes, **TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256** is supported.
-  Each Kafka broker allows a maximum of 1000 connections from each IP address by default. Excess connections will be rejected. You can change the limit by referring to :ref:`Modifying Kafka Instance Configuration Parameters <kafka-ug-0007>`, that is, to modify parameter **max.connections.per.ip**.

Prerequisites
-------------

-  The network between the client and the Kafka instance is available. For details about the network requirements, see :ref:`Kafka Network Connection Conditions <kafka-ug-180604012>`.

-  Security group rules have been properly configured.

   Before accessing a Kafka instance with ciphertext access enabled on a client, configure proper security group rules for the instance. For details, see :ref:`Table 2 <kafka-ug-180604012__table161395381402>`.

-  .. _kafka-ug-180801001__li10340528173815:

   The Kafka instance addresses have been obtained.

   Obtain the instance connection addresses in the **Connection** area on the **Basic Information** page on the Kafka console. The addresses are displayed in two types on the Kafka console. The one is **Private Network Access** or **Public Network Access** and the other is **Address (Private Network, Ciphertext)** or **Address (Public Network, Ciphertext)**.

   -  For **private access within a VPC**, the Kafka connection addresses are shown as follows.


      .. figure:: /_static/images/en-us_image_0000001756372046.png
         :alt: **Figure 1** Kafka instance addresses for private access within a VPC

         **Figure 1** Kafka instance addresses for private access within a VPC

   -  For **public access**, the Kafka connection addresses are shown as follows.


      .. figure:: /_static/images/en-us_image_0000001803290001.png
         :alt: **Figure 2** Kafka instance addresses for public access

         **Figure 2** Kafka instance addresses for public access

-  .. _kafka-ug-180801001__li198901524125317:

   The SASL mechanism in use is known.

   In the **Connection** area on the Kafka instance details page, view **SASL Mechanism**. For instances that were created much earlier, if **SASL Mechanism** is not displayed on the instance details page, PLAIN is used by default.


   .. figure:: /_static/images/en-us_image_0000001655285129.png
      :alt: **Figure 3** SASL mechanism in use

      **Figure 3** SASL mechanism in use

-  .. _kafka-ug-180801001__li112817505498:

   The security protocol in use is known.

   In the **Connection** area on the Kafka instance details page, view **Security Protocol**. For instances that were created much earlier, if **Security Protocol** is not displayed on the instance details page, SASL_SSL is used by default.

-  If automatic topic creation is not enabled for the Kafka instance, :ref:`create a topic <kafka-ug-180604018>` before connecting to the instance.

-  The **client.jks** certificate has been downloaded. Click the Kafka instance to go to the **Basic Information** tab page. Click **Download** next to **SSL Certificate** in the **Connection** area. Download and decompress the package to obtain the client certificate file **client.jks**.

   .. important::

      Later instances use the new certificate, and earlier ones use the old certificate. Later instances are incompatible with the old certificate, and earlier ones are incompatible with the new certificate.

      To determine whether a certificate is new, download the Zip file of the certificate on the console and see the file name. The earlier name is **kafka-certs.zip** and the later one is **kafka-cert-otc.zip**.

-  Compatible Kafka CLI is available. Ensure that the Kafka instance and the CLI use the same version.

   -  `Kafka CLI 1.1.0 <https://archive.apache.org/dist/kafka/1.1.0/kafka_2.11-1.1.0.tgz>`__
   -  `Kafka CLI 2.3.0 <https://archive.apache.org/dist/kafka/2.3.0/kafka_2.11-2.3.0.tgz>`__
   -  `Kafka CLI 2.7.2 <https://archive.apache.org/dist/kafka/2.7.2/kafka_2.12-2.7.2.tgz>`__
   -  `Kafka CLI 3.4.0 <https://archive.apache.org/dist/kafka/3.4.0/kafka_2.12-3.4.0.tgz>`__

-  `JDK v1.8.111 or later <https://www.oracle.com/java/technologies/downloads/#java8>`__ has been installed on the server, and the **JAVA_HOME** and **PATH** environment variables have been configured as follows:

   Add the following lines to the **.bash_profile** file in the home directory as an authorized user. In this command, **/opt/java/jdk1.8.0_151** is the JDK installation path. Change it to the path where you install JDK.

   .. code-block::

      export JAVA_HOME=/opt/java/jdk1.8.0_151
      export PATH=$JAVA_HOME/bin:$PATH

   Run the **source .bash_profile** command for the modification to take effect.

Accessing the Instance Using CLI
--------------------------------

The following uses Linux as an example.

#. Map hosts to IP addresses in the **/etc/hosts** file on the host where the client is located, so that the client can quickly parse the instance brokers.

   a. Run the following command to edit the **/etc/hosts** file:

      .. code-block::

         vim /etc/hosts

   b. Press **i** and add the mapping between the host and IP address to the **/etc/hosts** file.

      .. code-block::

         ip 1 host name 1
         ip 2 host name 2
         ip 3 host name 3

      .. table:: **Table 1** Parameters in the /etc/hosts file

         +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
         | Parameter                         | Description                                                                                                                   |
         +===================================+===============================================================================================================================+
         | ip                                | Connection address of the Kafka instance, which is obtained from :ref:`Prerequisites <kafka-ug-180801001__li10340528173815>`. |
         +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
         | host name                         | Name of each instance host.                                                                                                   |
         |                                   |                                                                                                                               |
         |                                   | Host names are user-defined and must be unique.                                                                               |
         +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------+

      For example:

      .. code-block::

         10.154.48.120 server01
         10.154.48.121 server02
         10.154.48.122 server03

   c. Press **Esc**. Enter the following line and press **Enter**. Save the **/etc/hosts** file and exit.

      .. code-block::

         :wq

#. Decompress the Kafka CLI package.

   Access the directory where the CLI package is stored and run the following command to decompress the package:

   .. code-block::

      tar -zxf {kafka_tar}

   In the preceding command, *{kafka_tar}* indicates the name of the CLI package.

   For example:

   .. code-block::

      tar -zxf kafka_2.12-2.7.2.tgz

#. .. _kafka-ug-180801001__li5414277457:

   Modify the configuration files of the Kafka CLI.

   Configuration files: **producer.properties** and **consumer.properties**

   **Modify the producer.properties file.**

   a. Go to the **/config** directory of the Kafka CLI.

      .. code-block::

         cd {kafka_tar}/config

   b. Edit the **producer.properties** file.

      .. code-block::

         vim producer.properties

   c. Press **i** and add the following content to the **producer.properties** file:

      #. Kafka instances support two authentication mechanisms. Add the one obtained in :ref:`SASL authentication mechanism <kafka-ug-180801001__li198901524125317>` to the configuration file. If both SCRAM-SHA-512 and PLAIN are enabled, use either of them in connection configurations.

         -  **PLAIN:**

            .. code-block::

               sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required \
               username="**********" \
               password="**********";
               sasl.mechanism=PLAIN

            .. table:: **Table 2** SASL authentication mechanism parameters

               ========= ==========================================
               Parameter Description
               ========= ==========================================
               username  Set in instance creation or user creation.
               password  Set in instance creation or user creation.
               ========= ==========================================

         -  **SCRAM-SHA-512:**

            .. code-block::

               sasl.jaas.config=org.apache.kafka.common.security.scram.ScramLoginModule required \
               username="**********" \
               password="**********";
               sasl.mechanism=SCRAM-SHA-512

            .. table:: **Table 3** SASL authentication mechanism parameters

               ========= ==========================================
               Parameter Description
               ========= ==========================================
               username  Set in instance creation or user creation.
               password  Set in instance creation or user creation.
               ========= ==========================================

      #. Kafka instances support two security protocols. Add the one obtained in :ref:`the security protocol <kafka-ug-180801001__li112817505498>` to the configuration file.

         -  **SASL_SSL:**

            .. code-block::

               security.protocol=SASL_SSL
               ssl.truststore.location={ssl_truststore_path}
               ssl.truststore.password=dms@kafka
               ssl.endpoint.identification.algorithm=

            .. table:: **Table 4** SASL_SSL parameters

               +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
               | Parameter                             | Description                                                                                                                                                                                                    |
               +=======================================+================================================================================================================================================================================================================+
               | ssl.truststore.location               | Path for storing the **client.jks** certificate                                                                                                                                                                |
               |                                       |                                                                                                                                                                                                                |
               |                                       | Even in Windows, you need to use slashes (/) for the certificate path. Do not use backslashes (\\), which are used by default for paths in Windows. Otherwise, the client will fail to obtain the certificate. |
               +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
               | ssl.truststore.password               | Password of the Kafka client certificate.                                                                                                                                                                      |
               |                                       |                                                                                                                                                                                                                |
               |                                       | **dms@kafka by default and cannot be changed.**                                                                                                                                                                |
               +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
               | ssl.endpoint.identification.algorithm | Whether to verify the certificate domain name **This parameter must be left blank, which indicates disabling domain name verification**.                                                                       |
               +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

         -  **SASL_PLAINTEXT:**

            .. code-block::

               security.protocol=SASL_PLAINTEXT

   d. Press **Esc**. Enter the following line and press **Enter**. Save the **producer.properties** file and exit.

      .. code-block::

         :wq

   **Modify the consumer.properties file.**

   a. Edit the **consumer.properties** file.

      .. code-block::

         vim consumer.properties

   b. Press **i** and add the following content to the **consumer.properties** file:

      #. Kafka instances support two authentication mechanisms. Add the one obtained in :ref:`SASL authentication mechanism <kafka-ug-180801001__li198901524125317>` to the configuration file. If both SCRAM-SHA-512 and PLAIN are enabled, use either of them in connection configurations.

         -  **PLAIN:**

            .. code-block::

               sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required \
               username="**********" \
               password="**********";
               sasl.mechanism=PLAIN

            .. table:: **Table 5** SASL authentication mechanism parameters

               ========= ==========================================
               Parameter Description
               ========= ==========================================
               username  Set in instance creation or user creation.
               password  Set in instance creation or user creation.
               ========= ==========================================

         -  **SCRAM-SHA-512:**

            .. code-block::

               sasl.jaas.config=org.apache.kafka.common.security.scram.ScramLoginModule required \
               username="**********" \
               password="**********";
               sasl.mechanism=SCRAM-SHA-512

            .. table:: **Table 6** SASL authentication mechanism parameters

               ========= ==========================================
               Parameter Description
               ========= ==========================================
               username  Set in instance creation or user creation.
               password  Set in instance creation or user creation.
               ========= ==========================================

      #. Kafka instances support two security protocols. Add the one obtained in :ref:`the security protocol <kafka-ug-180801001__li112817505498>` to the configuration file.

         -  **SASL_SSL:**

            .. code-block::

               security.protocol=SASL_SSL
               ssl.truststore.location={ssl_truststore_path}
               ssl.truststore.password=dms@kafka
               ssl.endpoint.identification.algorithm=

            .. table:: **Table 7** SASL_SSL parameters

               +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
               | Parameter                             | Description                                                                                                                                                                                                    |
               +=======================================+================================================================================================================================================================================================================+
               | ssl.truststore.location               | Path for storing the **client.jks** certificate                                                                                                                                                                |
               |                                       |                                                                                                                                                                                                                |
               |                                       | Even in Windows, you need to use slashes (/) for the certificate path. Do not use backslashes (\\), which are used by default for paths in Windows. Otherwise, the client will fail to obtain the certificate. |
               +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
               | ssl.truststore.password               | Password of the Kafka client certificate.                                                                                                                                                                      |
               |                                       |                                                                                                                                                                                                                |
               |                                       | **dms@kafka by default and cannot be changed.**                                                                                                                                                                |
               +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
               | ssl.endpoint.identification.algorithm | Whether to verify the certificate domain name **This parameter must be left blank, which indicates disabling domain name verification**.                                                                       |
               +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

         -  **SASL_PLAINTEXT:**

            .. code-block::

               security.protocol=SASL_PLAINTEXT

   c. Press **Esc**. Enter the following line and press **Enter**. Save the **consumer.properties** file and exit.

      .. code-block::

         :wq

#. Access the **/bin** directory of the Kafka CLI.

   In Windows, you need to access the **/bin/windows** directory.

   .. code-block::

      cd ../bin

#. Run the following command to create messages:

   .. code-block::

      ./kafka-console-producer.sh --broker-list {connection addr} --topic {topic name} --producer.config ../config/producer.properties

   .. table:: **Table 8** Message production parameters

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                            |
      +===================================+========================================================================================================================================================+
      | Connection Address                | Connection address of the Kafka instance.                                                                                                              |
      |                                   |                                                                                                                                                        |
      |                                   | Obtained in :ref:`Prerequisites <kafka-ug-180801001__li10340528173815>`.                                                                               |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Topic Name                        | The name of the topic created for the Kafka instance.                                                                                                  |
      |                                   |                                                                                                                                                        |
      |                                   | If automatic topic creation is enabled for the Kafka instance, set this parameter to the name of a created topic or a topic that has not been created. |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+

   The following example uses connection addresses **10.xx.xx.45:9095,10.xx.xx.127:9095,10.xx.xx.103:9095**.

   After running the preceding command, you can send a message to the Kafka instance by writing it and pressing **Enter**. Each line of content is sent as a message.

   .. code-block:: console

      [root@ecs-kafka bin]#./kafka-console-producer.sh --broker-list 10.xx.xx.45:9095,10.xx.xx.127:9095,10.xx.xx.103:9095  --topic topic-demo --producer.config ../config/producer.properties
      >Hello
      >DMS
      >Kafka!
      >^C[root@ecs-kafka bin]#

   To stop producing messages, press **Ctrl**\ +\ **C** to exit.

#. Run the following command to retrieve messages:

   .. code-block::

      ./kafka-console-consumer.sh --bootstrap-server {connection-address} --topic {topic-name} --group {consumer-group-name} --from-beginning  --consumer.config ../config/consumer.properties

   .. table:: **Table 9** Message consumption parameters

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                         |
      +===================================+=====================================================================================================================================================================================================================+
      | Connection Address                | Connection address of the Kafka instance.                                                                                                                                                                           |
      |                                   |                                                                                                                                                                                                                     |
      |                                   | Obtained in :ref:`Prerequisites <kafka-ug-180801001__li10340528173815>`.                                                                                                                                            |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Topic Name                        | The name of the topic created for the Kafka instance.                                                                                                                                                               |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Consumer Group Name               | The consumer group name set based on your service requirements. If a consumer group name starts with a special character, for example, an underscore (_) or a number sign (#), monitoring data cannot be displayed. |
      |                                   |                                                                                                                                                                                                                     |
      |                                   | .. warning::                                                                                                                                                                                                        |
      |                                   |                                                                                                                                                                                                                     |
      |                                   |    Ensure that the consumer group name in the command line is the same as that specified in the configuration file (**consumer.properties**), if any. Otherwise, message consumption may fail.                      |
      |                                   |                                                                                                                                                                                                                     |
      |                                   |    To view and change the consumer group name in the configuration file, see :ref:`6.a <kafka-ug-180801001__li117471450133610>`.                                                                                    |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   **To view and change the consumer group name in the configuration file:**

   a. .. _kafka-ug-180801001__li117471450133610:

      Access the **/config** directory of the Kafka CLI.

      .. code-block::

         cd ../config

   b. Edit the **consumer.properties** file.

      .. code-block::

         vim consumer.properties

   c. Press **i** to view and change the consumer group name.

      **group.id** indicates the consumer group name. You can change the name as required.

      .. code-block::

         # consumer group id
         group.id=test-consumer-group

   d. Press **Esc**. Enter the following line and press **Enter**. Save the **consumer.properties** file and exit.

      .. code-block::

         :wq

   Sample message consumption:

   .. code-block:: console

      [root@ecs-kafka bin]#  ./kafka-console-consumer.sh --bootstrap-server 10.xx.xx.45:9095,10.xx.xx.127:9095,10.xx.xx.103:9095 --topic topic-demo --group order-test --from-beginning --consumer.config ../config/consumer.properties
      Hello
      DMS
      Kafka!
      ^CProcessed a total of 3 messages
      [root@ecs-kafka bin]#

   To stop consuming messages, press **Ctrl**\ +\ **C** to exit.
