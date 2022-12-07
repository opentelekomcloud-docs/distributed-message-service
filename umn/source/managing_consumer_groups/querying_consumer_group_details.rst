:original_name: kafka_ug_0021.html

.. _kafka_ug_0021:

Querying Consumer Group Details
===============================

View the consumer group list, consumer list, and consumer offsets.

Prerequisites
-------------

The consumer list can be viewed only when consumers in a consumer group are connected to the Kafka instance (that is, the consumer group is in the **STABLE** state).

Viewing the Consumer Group List (Console)
-----------------------------------------

#. Log in to the management console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view its details.

#. In the navigation pane, choose the **Consumer Groups** tab.

   The consumer group name, status, and Coordinator are displayed. **Coordinator** indicates the broker where the coordinator component is located. The consumer group status can be:

   -  **DEAD**: The consumer group has no member or metadata.
   -  **EMPTY**: The consumer group has metadata but has no member.
   -  **PREPARING_REBALANCE**: The consumer group is to be rebalanced.
   -  **COMPLETING_REBALANCE**: All members have joined the consumer group.
   -  **STABLE**: Members in the consumer group can consume messages normally.

#. (Optional) To query a specific consumer group, enter the consumer group name in the search box and click |image2|.

#. (Optional) To refresh the consumer group list, click |image3| in the upper right corner.

Viewing the Consumer Group List (Kafka CLI)
-------------------------------------------

-  If SASL is not enabled for the Kafka instance, run the following command in the **/**\ *{directory where the CLI is located}*\ **/kafka_{version}/bin/** directory to query the consumer group list:

   .. code-block::

      ./kafka-consumer-groups.sh --bootstrap-server {broker_ip}:{port} --list

-  If SASL has been enabled for the Kafka instance, perform the following steps to query the consumer group list:

   #. (Optional) If the SSL certificate configuration has been set, skip this step. Otherwise, perform the following operations:

      Create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client and add the SSL certificate configurations by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.

   #. Run the following command in the **/**\ *{directory where the CLI is located}*\ **/kafka_{version}/bin/** directory to query the consumer group list:

      .. code-block::

         ./kafka-consumer-groups.sh --bootstrap-server {broker_ip}:{port} --list --command-config ./config/ssl-user-config.properties

Viewing the Consumer List (Console)
-----------------------------------

#. Log in to the management console.

#. Click |image4| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view its details.

#. In the navigation pane, choose the **Consumer Groups** tab.

#. Click the name of the desired consumer group.

#. On the **Consumers** tab page, view the consumer list.

   In the consumer list, you can view the consumer ID, consumer address, and client ID.

#. (Optional) To query a specific consumer, enter the consumer ID in the search box and click |image5|.

Viewing the Consumer List (Kafka CLI)
-------------------------------------

-  If SASL is not enabled for the Kafka instance, run the following command in the **/**\ *{directory where the CLI is located}*\ **/kafka_{version}/bin/** directory to query the consumer list:

   .. code-block::

      ./kafka-consumer-groups.sh --bootstrap-server {broker_ip}:{port} --group {group_name} --members --describe

-  If SASL has been enabled for the Kafka instance, perform the following steps to query the consumer list:

   #. (Optional) If the SSL certificate configuration has been set, skip this step. Otherwise, perform the following operations:

      Create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client and add the SSL certificate configurations by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.

   #. Run the following command in the **/**\ *{directory where the CLI is located}*\ **/kafka_{version}/bin/** directory to query the consumer list:

      .. code-block::

         ./kafka-consumer-groups.sh --bootstrap-server {broker_ip}:{port} --group {group_name} --members --describe --command-config ./config/ssl-user-config.properties

Viewing Consumer Offsets (Console)
----------------------------------

#. Log in to the management console.
#. Click |image6| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired Kafka instance to view its details.
#. In the navigation pane, choose the **Consumer Groups** tab.
#. Click the name of the desired consumer group.
#. On the **Consumer Offset** tab page, view the list of topics that the consumer group has subscribed to, total number of messages accumulated in the topic, number of messages accumulated in each partition of the topic, offset of each partition, and latest offset.
#. (Optional) To query the consumer offsets of a specific topic, enter the topic name in the search box and click |image7|.

Viewing Consumer Offsets (Kafka CLI)
------------------------------------

-  If SASL is not enabled for the Kafka instance, run the following command in the **/**\ *{directory where the CLI is located}*\ **/kafka_{version}/bin/** directory to query consumer offsets:

   .. code-block::

      ./kafka-consumer-groups.sh --bootstrap-server {broker_ip}:{port} --offsets --describe --all-groups

-  If SASL has been enabled for the Kafka instance, perform the following steps to query consumer offsets:

   #. (Optional) If the SSL certificate configuration has been set, skip this step. Otherwise, perform the following operations:

      Create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client and add the SSL certificate configurations by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.

   #. Run the following command in the **/**\ *{directory where the CLI is located}*\ **/kafka_{version}/bin/** directory to query consumer offsets:

      .. code-block::

         ./kafka-consumer-groups.sh --bootstrap-server {broker_ip}:{port} --offsets --describe --all-groups --command-config ./config/ssl-user-config.properties

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0000001378919582.png
.. |image3| image:: /_static/images/en-us_image_0000001206335999.png
.. |image4| image:: /_static/images/en-us_image_0143929918.png
.. |image5| image:: /_static/images/en-us_image_0000001378919582.png
.. |image6| image:: /_static/images/en-us_image_0143929918.png
.. |image7| image:: /_static/images/en-us_image_0000001378919582.png
