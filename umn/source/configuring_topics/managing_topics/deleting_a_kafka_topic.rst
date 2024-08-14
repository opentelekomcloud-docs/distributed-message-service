:original_name: kafka-ug-180604019.html

.. _kafka-ug-180604019:

Deleting a Kafka Topic
======================

Delete a topic using either of the following methods:

-  :ref:`Deleting a Kafka Topic (Console) <kafka-ug-180604019__section0249155910409>`
-  :ref:`Deleting a Kafka Topic on the Client <kafka-ug-180604019__section98152410712>`

Prerequisites
-------------

-  A Kafka instance has been created, and a topic has been created in this instance.
-  The Kafka instance is in the **Running** state.

Constraint
----------

If your Kafka instances are connected using Logstash, stop Logstash before deleting topics. Otherwise, services may crash.

.. _kafka-ug-180604019__section0249155910409:

Deleting a Kafka Topic (Console)
--------------------------------

#. Log in to the console.
#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired Kafka instance to view the instance details.
#. In the navigation pane, choose **Topics**.
#. Delete topics using either of the following methods:

   -  Select one or more topics and click **Delete Topic** in the upper left corner.
   -  In the row containing the topic you want to delete, choose **More** > **Delete**.

#. In the **Delete Topic** dialog box that is displayed, click **OK** to delete the topic.

.. _kafka-ug-180604019__section98152410712:

Deleting a Kafka Topic on the Client
------------------------------------

If your Kafka client version is later than 2.2, you can use **kafka-topics.sh** to delete topics.

.. important::

   For an instance with ciphertext access enabled, if **allow.everyone.if.no.acl.found** is set to **false**, topics cannot be deleted through the client.

-  For a Kafka instance with ciphertext access disabled, run the following command in the **/bin** directory of the Kafka client:

   .. code-block::

      ./kafka-topics.sh --bootstrap-server ${connection-address} --delete --topic ${topic-name}

   Parameter description:

   -  **connection-address**: can be obtained from the **Connection** area on the **Basic Information** page on the Kafka console.
   -  **topic-name**: topic name.

   Example:

   .. code-block:: console

      [root@ecs-kafka bin]# ./kafka-topics.sh --bootstrap-server 192.168.xx.xx:9092,192.168.xx.xx:9092,192.168.xx.xx:9092 --delete --topic topic-01
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

         ./kafka-topics.sh --bootstrap-server ${connection-address} --delete --topic ${topic-name} --command-config ../config/ssl-user-config.properties

      Parameter description:

      -  **connection-address**: can be obtained from the **Connection** area on the **Basic Information** page on the Kafka console.
      -  **topic-name**: topic name.

      Example:

      .. code-block:: console

         [root@ecs-kafka bin]# ./kafka-topics.sh --bootstrap-server 192.168.xx.xx:9093,192.168.xx.xx:9093,192.168.xx.xx:9093 --delete --topic topic-01 --command-config ../config/ssl-user-config.properties
         [root@ecs-kafka bin]#

.. |image1| image:: /_static/images/en-us_image_0143929918.png
