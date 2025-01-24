:original_name: kafka-ug-0006.html

.. _kafka-ug-0006:

Changing Kafka Partition Quantity
=================================

After creating a topic, you can increase the number of partitions as required.

.. note::

   Changing the number of partitions does not restart the instance or affect services.

Methods for changing the partition quantity:

-  :ref:`Modifying Topic Partitions on the Console <kafka-ug-0006__section11349555102717>`
-  :ref:`Modifying Topic Partitions on the Client <kafka-ug-0006__section2227184716161>`

.. _kafka-ug-0006__section11349555102717:

Modifying Topic Partitions on the Console
-----------------------------------------

#. Log in to the console.
#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired Kafka instance to view the instance details.
#. In the navigation pane, choose **Topics**.
#. Modify the number of partitions using either of the following methods:

   -  Select one or more topics and click **Edit Topic** in the upper left corner.
   -  In the row containing the desired topic, click **Edit**.

#. In the **Edit Topic** dialog box, enter the number of partitions and click **OK**.

   .. note::

      -  The number of partitions can only be increased.
      -  To ensure performance, the Kafka console allows a maximum of 200 partitions for each topic.
      -  The total partitions of all topics cannot exceed the maximum partitions of an instance. The maximum partitions of an instance vary by instance specifications. For details, see :ref:`Specifications <kafka-specification>`.

.. _kafka-ug-0006__section2227184716161:

Modifying Topic Partitions on the Client
----------------------------------------

If your Kafka client version is later than 2.2, you can use **kafka-topics.sh** to change the partition quantity.

.. important::

   For an instance with ciphertext access enabled, if **allow.everyone.if.no.acl.found** is set to **false**, topic partition quantity cannot be modified through the client.

-  For a Kafka instance with ciphertext access disabled, run the following command in the **/bin** directory of the Kafka client:

   .. code-block::

      ./kafka-topics.sh --bootstrap-server ${connection-address} --topic ${topic-name} --alter --partitions ${number-of-partitions}

   Parameter description:

   -  **connection-address**: can be obtained from the **Connection** area on the **Basic Information** page on the Kafka console.
   -  **topic-name**: topic name.
   -  **number-of-partitions**: number of partitions in a topic. To ensure performance, a partition number within 200 is recommended for each topic.

   Example:

   .. code-block:: console

      [root@ecs-kafka bin]# ./kafka-topics.sh --bootstrap-server 192.168.xx.xx:9092,192.168.xx.xx:9092,192.168.xx.xx:9092 --topic topic-01 --alter --partitions 6
      [root@ecs-kafka bin]#

-  For a Kafka instance with ciphertext access enabled, do as follows:

   #. (Optional) Modify the client configuration file.

      View **Security Protocol** in the **Connection** area on the **Basic Information** page on the Kafka console. The configuration settings vary depending on the protocol.

      -  SASL_PLAINTEXT: Skip this step and go to :ref:`2 <kafka-ug-0006__li529219395271>` if the username and password are already set. Otherwise, create the **ssl-user-config.properties** file in the **/config** directory on the Kafka client and add the following content to the file:

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

      -  SASL_SSL: Skip this step and go to :ref:`2 <kafka-ug-0006__li529219395271>` if the username, password, and SSL certificate are already set. Otherwise, create the **ssl-user-config.properties** file in the **/config** directory on the Kafka client and add the following content to the file:

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

   #. .. _kafka-ug-0006__li529219395271:

      Run the following command in the **/bin** directory of the Kafka client:

      .. code-block::

         ./kafka-topics.sh --bootstrap-server ${connection-address} --topic ${topic-name} --alter --partitions ${number-of-partitions} --command-config ../config/ssl-user-config.properties

      Parameter description:

      -  **connection-address**: can be obtained from the **Connection** area on the **Basic Information** page on the Kafka console.
      -  **topic-name**: topic name.
      -  **number-of-partitions**: number of partitions in a topic. To ensure performance, a partition number within 200 is recommended for each topic.

      Example:

      .. code-block:: console

         [root@ecs-kafka bin]# ./kafka-topics.sh --bootstrap-server 192.168.xx.xx:9093,192.168.xx.xx:9093,192.168.xx.xx:9093 --topic topic-01 --alter --partitions 6 --command-config ../config/ssl-user-config.properties
         [root@ecs-kafka bin]#

.. |image1| image:: /_static/images/en-us_image_0143929918.png
