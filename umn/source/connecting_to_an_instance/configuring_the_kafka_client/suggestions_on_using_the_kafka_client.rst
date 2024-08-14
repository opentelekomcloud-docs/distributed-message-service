:original_name: Kafka-client-best-practice.html

.. _Kafka-client-best-practice:

Suggestions on Using the Kafka Client
=====================================

Consumers
---------

#. Ensure that the owner thread does not exit abnormally. Otherwise, the client may fail to initiate consumption requests and the consumption will be blocked.
#. Commit messages only after they have been processed. Otherwise, the messages may fail to be processed and cannot be polled again.
#. Generally, do not commit every message. Otherwise, there will be many **OFFSET_COMMIT** requests, causing high CPU usage. For example, if a consumption request pulls 1000 messages and commits every one of them, TPS of the commit requests is 1000 times that of consumption. The smaller the message size, the larger the ratio. You can commit a specific number of messages in batches or enable **enable.auto.commit**. However, if the client is faulty, some cached consumption offset may be lost, resulting in repeated consumption. Therefore, you are advised to commit messages in batches based on service requirements.
#. A consumer cannot frequently join or leave a group. Otherwise, the consumer will frequently perform rebalancing, which blocks consumption.
#. The number of consumers cannot be greater than the number of partitions in the topic. Otherwise, some consumers may fail to poll for messages.
#. Ensure that the consumer polls at regular intervals to keep sending heartbeats to the server. If the consumer stops sending heartbeats for long enough, the consumer session will time out and the consumer will be considered to have stopped. This will also block consumption.
#. Ensure that there is a limitation on the size of messages buffered locally to avoid an out-of-memory (OOM) situation.
#. Set the timeout for the consumer session to 30 seconds: session.timeout.ms=30000.
#. Kafka supports exactly-once delivery. Therefore, ensure the idempotency of processing messages for services.
#. Always close the consumer before exiting. Otherwise, consumers in the same group may be blocked within the timeout set by **session.timeout.ms**.
#. Do not start a consumer group name with a special character, such as a number sign (#). Otherwise, monitoring data of the consumer group cannot be displayed.

Producers
---------

#. Synchronous replication: Set **acks** to **all**.
#. Retry message sending: Set **retries** to **3**.
#. Optimize message sending: For latency-sensitive messages, set **linger.ms** to **0**. For latency-insensitive messages, set **linger.ms** to a value ranging from **100** to **1000**.
#. Ensure that the producer has sufficient JVM memory to avoid blockages.
#. Set the timestamp to the local time. Messages will fail to age if the timestamp is a future time.

Topics
------

Recommended topic configurations: Use 3 replicas, enable synchronous replication, and set the minimum number of in-sync replicas to 2. The number of in-sync replicas cannot be the same as the number of replicas of the topic. Otherwise, if one replica is unavailable, messages cannot be produced.

You can enable or disable automatic topic creation. If automatic topic creation is enabled, the system automatically creates a topic when a message is produced in or consumed from a topic that does not exist. This topic has the following default settings: 3 partitions, 3 replicas, aging time 72 hours, synchronous replication and flushing disabled, **CreateTime** message timestamp, and maximum 10,485,760 bytes message size.

Others
------

Maximum number of connections: 3000

Maximum size of a message: 10 MB

Access Kafka using SASL_SSL. Ensure that your DNS service is capable of resolving an IP address to a domain name. Alternatively, map all Kafka broker IP addresses to host names in the **hosts** file. Prevent Kafka clients from performing reverse resolution. Otherwise, connections may fail to be established.

Apply for a disk space size that is more than twice the size of service data multiplied by the number of replicas. In other words, keep 50% of the disk space idle.

Avoid frequent full GC in JVM. Otherwise, message production and consumption will be blocked.
