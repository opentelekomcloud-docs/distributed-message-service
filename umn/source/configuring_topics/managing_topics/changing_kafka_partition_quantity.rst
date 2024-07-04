:original_name: kafka-ug-0006.html

.. _kafka-ug-0006:

Changing Kafka Partition Quantity
=================================

After creating a topic, you can increase the number of partitions as required.

.. note::

   Changing the number of partitions does not restart the instance or affect services.

Methods for changing the partition quantity:

-  :ref:`Method 1: By using Kafka console <kafka-ug-0006__section11349555102717>`
-  :ref:`Method 2: By using Kafka CLI <kafka-ug-0006__section2227184716161>`

.. _kafka-ug-0006__section11349555102717:

Method 1: By using Kafka console
--------------------------------

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
      -  The total number of partitions of all topics cannot exceed the maximum number of partitions allowed by the instance.

.. _kafka-ug-0006__section2227184716161:

Method 2: By Using Kafka CLI
----------------------------

If your Kafka client version is later than 2.2, you can use **kafka-topics.sh** to change the partition quantity.

.. important::

   For an instance with ciphertext access enabled, if **allow.everyone.if.no.acl.found** is set to **false**, topic partition quantity cannot be modified through the client.

-  For a Kafka instance with ciphertext access disabled, run the following command in the **/bin** directory of the Kafka client:

   .. code-block::

      ./kafka-topics.sh --bootstrap-server ${connection-address} --topic ${topic-name} --alter --partitions ${number-of-partitions}

-  For a Kafka instance with ciphertext access enabled, do as follows:

   #. (Optional) For the Kafka security protocol, is SASL_PLAINTEXT or SASL_SSL used?

      -  SASL_PLAINTEXT: Skip this step if the username and password are already set. In other cases, create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client. Add the username and password by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.
      -  SASL_SSL: Skip this step if the username, password, and SSL certificate are already set. In other cases, create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client. Add the username and password, and the SSL certificate configuration by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.

   #. Run the following command in the **/bin** directory of the Kafka client:

      .. code-block::

         ./kafka-topics.sh --bootstrap-server ${connection-address} --topic ${topic-name} --alter --partitions ${number-of-partitions} --command-config ./config/ssl-user-config.properties

.. |image1| image:: /_static/images/en-us_image_0143929918.png
