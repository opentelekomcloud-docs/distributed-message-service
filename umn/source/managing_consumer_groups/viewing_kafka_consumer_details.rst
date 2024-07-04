:original_name: kafka-ug-0015.html

.. _kafka-ug-0015:

Viewing Kafka Consumer Details
==============================

This section describes how to view the consumer list and consumer connection addresses.

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

#. Click the desired Kafka instance to view the instance details.

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

-  For a Kafka instance with ciphertext access enabled, do as follows:

   #. (Optional) For the Kafka security protocol, is SASL_PLAINTEXT or SASL_SSL used?

      -  SASL_PLAINTEXT: Skip this step if the username and password are already set. In other cases, create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client. Add the username and password by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.
      -  SASL_SSL: Skip this step if the username, password, and SSL certificate are already set. In other cases, create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client. Add the username and password, and the SSL certificate configuration by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.

   #. Run the following command in the **/bin** directory of the Kafka client:

      .. code-block::

         ./kafka-consumer-groups.sh --bootstrap-server ${connection-address} --group ${group-name} --members --describe --command-config ./config/ssl-user-config.properties

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
