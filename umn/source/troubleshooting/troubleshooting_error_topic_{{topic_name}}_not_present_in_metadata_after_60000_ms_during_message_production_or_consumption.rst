:original_name: kafka-trouble-0004.html

.. _kafka-trouble-0004:

Troubleshooting Error "Topic {{topic_name}} not present in metadata after 60000 ms" During Message Production or Consumption
============================================================================================================================

Symptom
-------

For a Kafka instance deployed in multiple AZs, if one of the AZs is faulty, error message "Topic {{topic_name}} not present in metadata after 60000 ms" may be reported on the Kafka client during message production or consumption, as shown in the following figure.

|image1|

Solution
--------

You can use any of the following methods to solve this problem:

-  Upgrade the Kafka client to v2.7 or later, and set **socket.connection.setup.timeout.ms** to a value greater than 1s and less than the value of **request.timeout.ms** divided by the number of Kafka server nodes. To obtain the number of Kafka server brokers:

   #. Log in to the DMS console.
   #. Click a Kafka instance. On the instance details page that is displayed, view the value of **Private Network Access** in the **Connection** area. The number of connection addresses next to **Address** is the number of Kafka server brokers.

-  Change the value of **request.timeout.ms** of the Kafka client to a value greater than 127s.
-  Change the Linux network parameter **net.ipv4.tcp_syn_retries** of the Kafka client to **3**.

.. |image1| image:: /_static/images/en-us_image_0000001174310752.png
