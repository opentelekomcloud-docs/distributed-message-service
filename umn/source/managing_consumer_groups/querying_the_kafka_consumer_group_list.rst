:original_name: kafka_ug_0021.html

.. _kafka_ug_0021:

Querying the Kafka Consumer Group List
======================================

This section describes how to query the consumer group list.

Viewing the Consumer Group List (Console)
-----------------------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view its details.

#. In the navigation pane, choose the **Consumer Groups** tab.

   The consumer group name, status, and Coordinator (ID) are displayed. Coordinator (ID) indicates the broker where the coordinator component is located. The consumer group status can be:

   -  **DEAD**: The consumer group has no member or metadata.
   -  **EMPTY**: The consumer group has metadata but has no member.
   -  **PREPARING_REBALANCE**: The consumer group is to be rebalanced.
   -  **COMPLETING_REBALANCE**: All members have joined the consumer group.
   -  **STABLE**: Members in the consumer group can consume messages normally.

#. (Optional) To query a consumer group, enter a consumer group name or status, Coordinator (ID), or keyword, then press **Enter**.

#. (Optional) To refresh the consumer group list, click |image2| in the upper right corner.

Viewing the Consumer Group List (Kafka CLI)
-------------------------------------------

-  For a Kafka instance with ciphertext access disabled, run the following command in the **/bin** directory of the Kafka client:

   .. code-block::

      ./kafka-consumer-groups.sh --bootstrap-server ${connection-address} --list

-  For a Kafka instance with ciphertext access enabled, do as follows:

   #. (Optional) For the Kafka security protocol, is SASL_PLAINTEXT or SASL_SSL used?

      -  SASL_PLAINTEXT: Skip this step if the username and password are already set. In other cases, create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client. Add the username and password by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.
      -  SASL_SSL: Skip this step if the username, password, and SSL certificate are already set. In other cases, create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client. Add the username and password, and the SSL certificate configuration by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.

   #. Run the following command in the **/bin** directory of the Kafka client:

      .. code-block::

         ./kafka-consumer-groups.sh --bootstrap-server ${connection-address} --list --command-config ./config/ssl-user-config.properties

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0000001206335999.png
