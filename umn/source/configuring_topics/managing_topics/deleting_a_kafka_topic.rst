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

-  For a Kafka instance with ciphertext access enabled, do as follows:

   #. (Optional) For the Kafka security protocol, is SASL_PLAINTEXT or SASL_SSL used?

      -  SASL_PLAINTEXT: Skip this step if the username and password are already set. In other cases, create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client. Add the username and password by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.
      -  SASL_SSL: Skip this step if the username, password, and SSL certificate are already set. In other cases, create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client. Add the username and password, and the SSL certificate configuration by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.

   #. Run the following command in the **/bin** directory of the Kafka client:

      .. code-block::

         ./kafka-topics.sh --bootstrap-server ${connection-address} --delete --topic ${topic-name} --command-config ./config/ssl-user-config.properties

.. |image1| image:: /_static/images/en-us_image_0143929918.png
