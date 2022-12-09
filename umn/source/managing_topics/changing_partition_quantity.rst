:original_name: kafka-ug-0006.html

.. _kafka-ug-0006:

Changing Partition Quantity
===========================

After creating a topic, you can increase the number of partitions based on service requirements.

.. note::

   Changing the number of partitions does not affect services.

Methods for changing the partition quantity:

-  :ref:`Method 1: By Using the Console <kafka-ug-0006__section11349555102717>`
-  :ref:`Method 2: By using Kafka CLI <kafka-ug-0006__section2227184716161>`

.. _kafka-ug-0006__section11349555102717:

Method 1: By Using the Console
------------------------------

#. Log in to the management console.
#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired Kafka instance to view the instance details.
#. Click the **Topics** tab.
#. Modify the number of partitions using either of the following methods:

   -  Select one or more topics and click **Edit Topic** in the upper left corner.
   -  In the row containing the desired topic, click **Edit**.

#. In the **Edit Topic** dialog box, enter the number of partitions and click **OK**.

   .. note::

      -  The number of partitions can only be increased.
      -  To ensure performance, the Kafka console allows a maximum of 100 partitions for each topic.
      -  The total number of partitions of all topics cannot exceed the maximum number of partitions allowed by the instance.

.. _kafka-ug-0006__section2227184716161:

Method 2: By Using Kafka CLI
----------------------------

If your Kafka client version is later than 2.2, you can use **kafka-topics.sh** to change the partition quantity.

-  If SASL is not enabled for the Kafka instance, run the following command in the **/**\ *{directory where the CLI is located}*\ **/kafka_{version}/bin/** directory to change the partition quantity:

   .. code-block::

      ./kafka-topics.sh --bootstrap-server {broker_ip}:{port} --topic {topic_name} --alter --partitions {partition_num}

-  If SASL has been enabled for the Kafka instance, perform the following steps to change the partition quantity:

   #. (Optional) If the SSL certificate configuration has been set, skip this step. Otherwise, perform the following operations:

      Create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client and add the SSL certificate configurations by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.

   #. Run the following command in the **/**\ *{directory where the CLI is located}*\ **/kafka_{version}/bin/** directory to change the partition quantity:

      .. code-block::

         ./kafka-topics.sh --bootstrap-server {broker_ip}:{port} --topic {topic_name} --alter --partitions {partition_num} --command-config ./config/ssl-user-config.properties

.. |image1| image:: /_static/images/en-us_image_0143929918.png
