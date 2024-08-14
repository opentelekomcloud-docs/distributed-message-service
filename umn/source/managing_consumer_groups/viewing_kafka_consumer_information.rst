:original_name: kafka-ug-0015.html

.. _kafka-ug-0015:

Viewing Kafka Consumer Information
==================================

If a consumer group has consumers who are accessing a Kafka instance, you can view their connection information.

Prerequisites
-------------

The consumer list and connection address can be viewed only when consumers in a consumer group are connected to the Kafka instance (that is, the consumer group is in the **STABLE** state).

Viewing the Consumer List (Console)
-----------------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click an instance to go to the instance details page.

#. In the navigation pane, choose **Consumer Groups**.

#. Click the name of the desired consumer group.

#. On the **Consumers** tab page, view the consumer list.

   In the consumer list, you can view the consumer ID, consumer address, and client ID.

#. (Optional) To query a specific consumer, enter the consumer ID in the search box and press **Enter**.

Viewing the Consumer List (Kafka CLI)
-------------------------------------

-  For a Kafka instance with ciphertext access disabled, run the following command in the **/bin** directory of the Kafka client:

   .. code-block::

      ./kafka-consumer-groups.sh --bootstrap-server ${connection-address} --group ${group-name} --members --describe

   Parameter description:

   -  **connection-address**: can be obtained from the **Connection** area on the **Basic Information** page on the Kafka console.
   -  **group-name**: consumer group name.

   Example:

   .. code-block:: console

      [root@ecs-kafka bin]# ./kafka-consumer-groups.sh --bootstrap-server 192.168.xx.xx:9092,192.168.xx.xx:9092,192.168.xx.xx:9092 --group test --members --describe

      GROUP           CONSUMER-ID                                           HOST            CLIENT-ID        #PARTITIONS
      test            console-consumer-571a64fe-b0c4-47ce-833d-9e0da5a88d14 /192.168.0.215  console-consumer 3
      [root@ecs-kafka bin]#

-  For a Kafka instance with ciphertext access enabled, do as follows:

   #. (Optional) Modify the client configuration file.

      View **Security Protocol** in the **Connection** area on the **Basic Information** page on the Kafka console. The configuration settings vary depending on the protocol.

      -  SASL_PLAINTEXT: Skip this step if the username and password are already set. Otherwise, create the **ssl-user-config.properties** file in the **/config** directory on the Kafka client and add the following content to the file:

         .. code-block::

            security.protocol=SASL_PLAINTEXT
            # If the SASL mechanism is SCRAM-SHA-512, configure as follows:
            sasl.jaas.config=org.apache.kafka.common.security.scram.ScramLoginModule required \
            username="**********" \
            password="**********";
            sasl.mechanism=SCRAM-SHA-512
            # If the SASL mechanism is PLAIN, configure as follows:
            sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required \
            username="**********" \
            password="**********";
            sasl.mechanism=PLAIN

         Parameter description: **username** and **password** are the ones you set when enabling ciphertext access for the first time or when creating a user.

      -  SASL_SSL: Skip this step if the username, password, and SSL certificate are already set. Otherwise, create the **ssl-user-config.properties** file in the **/config** directory on the Kafka client and add the following content to the file:

         .. code-block::

            security.protocol=SASL_SSL
            ssl.truststore.location={ssl_truststore_path}
            ssl.truststore.password=dms@kafka
            ssl.endpoint.identification.algorithm=
            # If the SASL mechanism is SCRAM-SHA-512, configure as follows:
            sasl.jaas.config=org.apache.kafka.common.security.scram.ScramLoginModule required \
            username="**********" \
            password="**********";
            sasl.mechanism=SCRAM-SHA-512
            # If the SASL mechanism is PLAIN, configure as follows:
            sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required \
            username="**********" \
            password="**********";
            sasl.mechanism=PLAIN

         Parameter description:

         -  **ssl.truststore.location**: path for storing the **client.jks** certificate. Even in Windows, you need to use slashes (/) for the certificate path. Do not use backslashes (\\), which are used by default for paths in Windows. Otherwise, the client will fail to obtain the certificate.
         -  **ssl.truststore.password**: server certificate password, which must be set to **dms@kafka** and cannot be changed.
         -  **ssl.endpoint.identification.algorithm**: whether to verify the certificate domain name. **This parameter must be left blank, which indicates disabling domain name verification**.
         -  **username** and **password**: username and password you set when enabling ciphertext access for the first time or when creating a user.

   #. Run the following command in the **/bin** directory of the Kafka client:

      .. code-block::

         ./kafka-consumer-groups.sh --bootstrap-server ${connection-address} --group ${group-name} --members --describe --command-config ../config/ssl-user-config.properties

      Parameter description:

      -  **connection-address**: can be obtained from the **Connection** area on the **Basic Information** page on the Kafka console.
      -  **group-name**: consumer group name.

      Example:

      .. code-block:: console

         [root@ecs-kafka bin]# ./kafka-consumer-groups.sh --bootstrap-server 192.168.xx.xx:9093,192.168.xx.xx:9093,192.168.xx.xx:9093 --group test --members --describe --command-config ../config/ssl-user-config.properties

         GROUP           CONSUMER-ID                                           HOST            CLIENT-ID        #PARTITIONS
         test            console-consumer-566d0c82-07d3-4d87-9a6e-f57a9bc9fc69 /192.168.0.215  console-consumer 3
         [root@ecs-kafka bin]#

Viewing Consumer Connection Addresses (Console)
-----------------------------------------------

#. Log in to the console.
#. Click |image2| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired Kafka instance to view the instance details.
#. In the navigation pane, choose **Consumer Groups**.
#. Click the desired consumer group.
#. On the **Consumers** tab page, view the consumer addresses.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0143929918.png
