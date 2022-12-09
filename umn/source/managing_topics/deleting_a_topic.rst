:original_name: kafka-ug-180604019.html

.. _kafka-ug-180604019:

Deleting a Topic
================

Delete a topic using either of the following methods:

-  :ref:`By using the console <kafka-ug-180604019__section0249155910409>`
-  :ref:`By using Kafka CLI <kafka-ug-180604019__section98152410712>`

Prerequisites
-------------

-  A Kafka instance has been created, and a topic has been created in this instance.
-  The Kafka instance is in the **Running** state.

.. _kafka-ug-180604019__section0249155910409:

Deleting a Topic on the Console
-------------------------------

#. Log in to the management console.
#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired Kafka instance to view the instance details.
#. Click the **Topics** tab.
#. Delete topics using either of the following methods:

   -  Select one or more topics and click **Delete Topic** in the upper left corner.
   -  In the row containing the topic you want to delete, click **Delete**.

#. In the **Delete Topic** dialog box that is displayed, click **Yes** to delete the topic.

.. _kafka-ug-180604019__section98152410712:

Deleting a Topic with the Kafka CLI
-----------------------------------

If your Kafka client version is later than 2.2, you can use **kafka-topics.sh** to delete topics.

-  If SASL is not enabled for the Kafka instance, run the following command in the **/**\ *{directory where the CLI is located}*\ **/kafka_{version}/bin/** directory to delete a topic:

   .. code-block::

      ./kafka-topics.sh --bootstrap-server {broker_ip}:{port} --delete --topic {topic_name}

-  If SASL has been enabled for the Kafka instance, perform the following steps to delete a topic:

   #. (Optional) If the SSL certificate configuration has been set, skip this step. Otherwise, perform the following operations:

      Create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client and add the SSL certificate configurations by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.

   #. Run the following command in the **/**\ *{directory where the CLI is located}*\ **/kafka_{version}/bin/** directory to delete a topic:

      .. code-block::

         ./kafka-topics.sh --bootstrap-server {broker_ip}:{port} --delete --topic {topic_name} --command-config ./config/ssl-user-config.properties

.. |image1| image:: /_static/images/en-us_image_0143929918.png
