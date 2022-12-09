:original_name: kafka-scenarios.html

.. _kafka-scenarios:

Application Scenarios
=====================

Kafka is popular message-oriented middleware that features highly reliable, asynchronous message delivery. It is widely used for transmitting data between different systems in many industries, including enterprise application, payment, telecommunications, e-commerce, social networking, instant messaging, video, Internet of Things, and Internet of Vehicle.

Asynchronous Communication
--------------------------

Non-core or less important messages are sent asynchronously to receiving systems, so that the main service process is not kept waiting for the results of other systems, allowing for faster responses.

For example, Kafka can be used to send a notification email and SMS message after a user has registered with a website, providing fast responses throughout the registration process.


.. figure:: /_static/images/en-us_image_0169396010.png
   :alt: **Figure 1** Serial registration and notification

   **Figure 1** Serial registration and notification


.. figure:: /_static/images/en-us_image_0169396012.png
   :alt: **Figure 2** Asynchronous registration and notification using message queues

   **Figure 2** Asynchronous registration and notification using message queues

Traffic Control
---------------

In e-commerce systems or large-scale websites, there is a processing capability gap between upstream and downstream systems. Traffic bursts from upstream systems with high processing capabilities may have a large impact on downstream systems with lower processing capabilities. For example, online sales promotions involve a huge amount of traffic flooding into e-commerce systems. Kafka provides a three-day buffer by default for hundreds of millions of messages, such as orders and other information. In this way, message consumption systems can process the messages during off-peak periods.

In addition, flash sale traffic bursts originating from frontend systems can be handled with Kafka, keeping the backend systems from crashing.


.. figure:: /_static/images/en-us_image_0169396015.png
   :alt: **Figure 3** Traffic burst handling using Kafka

   **Figure 3** Traffic burst handling using Kafka

Log Synchronization
-------------------

In large-scale service systems, logs of different applications are collected for quick troubleshooting, full-link tracing, and real-time monitoring.

Kafka is originally designed for this scenario. Applications asynchronously send log messages to message queues over reliable transmission channels. Other components can read the log messages from message queues for further analysis, either in real time or offline. In addition, Kafka can collect key log information to monitor applications.

Log synchronization involves three major components: log collection clients, Kafka, and backend log processing applications.

#. The log collection clients collect log data from a user application service and asynchronously send the log data in batches to Kafka clients.

   Kafka clients receive and compress messages in batches. This only has a minor impact on the service performance.

#. Kafka persists logs.

#. Log processing applications, such as Logstash, subscribe to messages in Kafka and retrieve log messages from Kafka. Then, the messages are searched for by file search services or delivered to big data applications such as Hadoop for storage and analysis.


.. figure:: /_static/images/en-us_image_0169396006.png
   :alt: **Figure 4** Log synchronization process

   **Figure 4** Log synchronization process

.. note::

   Logstash is for log analytics, Elasticsearch is for log search, and Hadoop is for big data analytics. They are all open-source tools.
