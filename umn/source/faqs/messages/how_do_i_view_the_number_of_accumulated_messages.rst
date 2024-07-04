:original_name: kafka-faq-0041.html

.. _kafka-faq-0041:

How Do I View the Number of Accumulated Messages?
=================================================

View the number of accumulated messages using any of the following methods:

-  On the **Consumer Groups** page of an instance, click the name of the consumer group whose accumulated messages are to be viewed. The consumer group details page is displayed. On the **Consumer Offset** tab page, view the number of messages accumulated in each topic of your target consumer group. For details, see :ref:`Querying Consumer Group Details <kafka_ug_0021>`.

-  On the **Monitoring** tab page of an instance, click the **By Consumer Group** tab. Select the desired consumer group for **Consumer Group** and **All topics** for **Topic**. The **Consumer Available Messages** metric reflects the number of messages accumulated in all topics of this consumer group. For details about viewing the monitoring data, see :ref:`Viewing Metrics <kafka-ug-190605001>`.

-  On the **Consumer Groups** tab page of the Cloud Eye console, click the **By Consumer Group** tab. Select the desired consumer group for **Consumer Group** and **All topics** for **Topic**. The **Consumer Available Messages** metric reflects the number of messages accumulated in all topics of this consumer group. For details about viewing the monitoring data, see :ref:`Viewing Metrics <kafka-ug-190605001>`.

-  In the **/bin** directory on the `Kafka client <https://cwiki.apache.org/confluence/display/KAFKA/Clients>`__, run command **kafka-consumer-groups.sh --bootstrap-server $\ {connection-address} --describe --group $\ {consumer-group-name}** to check number of accumulated messages of each topic in a consumer group. **LAG** indicates the total number of messages accumulated in each topic.


   .. figure:: /_static/images/en-us_image_0000001435265813.png
      :alt: **Figure 1** Viewing the total number of messages accumulated in each topic

      **Figure 1** Viewing the total number of messages accumulated in each topic

   .. note::

      If SASL authentication is enabled for the Kafka instance, the **--command-config {SASL authentication configuration file consumer.properties}** parameter must be added to the preceding command. For details about the configuration file **consumer.properties**, see the CLI access instructions provided in :ref:`Accessing a Kafka Instance with SASL <kafka-ug-180801001>`.
