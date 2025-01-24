:original_name: kafka-ug-0012.html

.. _kafka-ug-0012:

Deleting a Kafka Consumer Group
===============================

You can delete a consumer group in either of the following ways:

-  On the console.
-  Use `Kafka CLI <https://cwiki.apache.org/confluence/display/KAFKA/Clients>`__. (Ensure that the Kafka instance version is the same as the CLI version.)

Constraints
-----------

-  If **auto.create.groups.enable** is set to **true**, the consumer group status is **EMPTY**, and no offset has been submitted, the system automatically deletes the consumer group 10 minutes later.
-  If **auto.create.groups.enable** is set to **false**, the system does not automatically delete consumer groups. You can manually delete them.
-  If a consumer group has never committed an offset, the group will be deleted after the Kafka instance restarts.

Prerequisites
-------------

The status of the consumer group to be deleted is **EMPTY**.

Deleting a Consumer Group on the Console
----------------------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view the instance details.

#. In the navigation pane, choose the **Consumer Groups** tab.

#. Delete consumer groups using either of the following methods:

   -  Select one or more consumer groups and click **Delete Consumer Group** above the consumer group list.
   -  In the row containing the consumer group you want to delete, click **Delete**.

   .. important::

      A consumer group can be deleted only when its status is **EMPTY**.

   Consumer group statuses include:

   -  **DEAD**: The consumer group has no member or metadata.
   -  **EMPTY**: The consumer group has metadata but has no member.
   -  **PREPARING_REBALANCE**: The consumer group is to be rebalanced.
   -  **COMPLETING_REBALANCE**: All members have joined the consumer group.
   -  **STABLE**: Members in the consumer group can consume messages normally.

#. In the displayed **Delete Consumer Group** dialog box, click **OK**.

Using the CLI to Delete a Consumer Group
----------------------------------------

The following uses Linux as an example.

-  For a Kafka instance with ciphertext access disabled, run the following command in the **/bin** directory of the Kafka client:

   .. code-block::

      ./kafka-consumer-groups.sh --bootstrap-server ${connection-address} --delete --group ${consumer-group-name}

   Parameter description:

   -  **connection-address**: can be obtained from the **Connection** area on the **Basic Information** page on the Kafka console.
   -  **consumer-group-name**: consumer group name.

   Example:

   .. code-block:: console

      [root@ecs-kafka bin]# ./kafka-consumer-groups.sh --bootstrap-server 192.168.xx.xx:9092,192.168.xx.xx:9092,192.168.xx.xx:9092 --delete --group group-01
      Deletion of requested consumer groups ('group-01') was successful.
      [root@ecs-kafka bin]#

-  For a Kafka instance with ciphertext access enabled, do as follows:

   #. (Optional) Modify the client configuration file.

      View **Security Protocol** in the **Connection** area on the **Basic Information** page on the Kafka console. The configuration settings vary depending on the protocol.

      -  SASL_PLAINTEXT: Skip this step and go to :ref:`2 <kafka-ug-0012__li529219395271>` if the username and password are already set. Otherwise, create the **ssl-user-config.properties** file in the **/config** directory on the Kafka client and add the following content to the file:

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

      -  SASL_SSL: Skip this step and go to :ref:`2 <kafka-ug-0012__li529219395271>` if the username, password, and SSL certificate are already set. Otherwise, create the **ssl-user-config.properties** file in the **/config** directory on the Kafka client and add the following content to the file:

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

   #. .. _kafka-ug-0012__li529219395271:

      In the **/bin** directory of the Kafka client, run the following command:

      .. code-block::

         ./kafka-consumer-groups.sh --bootstrap-server ${connection-address} --delete --group ${consumer-group-name} --command-config ../config/ssl-user-config.properties

      Parameter description:

      -  **connection-address**: can be obtained from the **Connection** area on the **Basic Information** page on the Kafka console.
      -  **consumer-group-name**: consumer group name.

      Example:

      .. code-block:: console

         [root@ecs-kafka bin]# ./kafka-consumer-groups.sh --bootstrap-server 192.168.xx.xx:9093,192.168.xx.xx:9093,192.168.xx.xx:9093 --delete --group group-02 --command-config ../config/ssl-user-config.properties
         Deletion of requested consumer groups ('group-02') was successful.
         [root@ecs-kafka bin]#

.. |image1| image:: /_static/images/en-us_image_0143929918.png
