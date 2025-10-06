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

#. The number of consumers in a consumer group must be within the total partitions subscribed by the consumer group. Otherwise, some consumers cannot pull messages.

#. Ensure that the consumer polls at regular intervals to keep sending heartbeats to the server. If the consumer stops sending heartbeats for long enough, the consumer session will time out and the consumer will be considered to have stopped. This will also block consumption.

#. Ensure that there is a limitation on the size of messages buffered locally to avoid an out-of-memory (OOM) situation.

#. Set the timeout for the consumer session to 30 seconds: session.timeout.ms=30000.

#. Kafka supports exactly-once delivery. Therefore, ensure the idempotency of processing messages for services.

#. Always close the consumer before exiting. Otherwise, consumers in the same group may be blocked within the timeout set by **session.timeout.ms**.

#. Do not start a consumer group name with a special character, such as a number sign (#). Otherwise, monitoring data of the consumer group cannot be displayed.

#. Handle AuthorizationException in the consumption logic and set consumption retry. For example, in SpringKafka, add the following configuration.

   .. code-block::

      # Set the authorization exception retry interval to 10 seconds.
      spring.kafka.listener.authorizationExceptionRetryInterval=10000

Producers
---------

#. Synchronous replication: Set **acks** to **all**.
#. Retry message sending: Set **retries** to **3**.
#. Optimize message sending: For latency-sensitive messages, set **linger.ms** to **0**. For latency-insensitive messages, set **linger.ms** to a value ranging from **100** to **1000**.
#. Ensure that the producer has sufficient JVM memory to avoid blockages.
#. Set the timestamp to the local time. Messages will fail to age if the timestamp is a future time.
#. Try reusing producers. Do not create producers frequently. When idempotence is enabled (default for producer clients 3.0 and later), producing messages creates producer state objects on the server. Frequent creation results in too many objects to be reclaimed in time, causing server memory surges and performance deterioration. Set **enable.idempotence** to **false** if the idempotence is not required.
#. Catch exception **AuthorizationException**. You are advised to retry message production on the service side. Self-healing can be implemented through limited retry and backoff policies.

Topics
------

Recommended topic configurations: Use 3 replicas, enable synchronous replication, and set the minimum number of in-sync replicas to 2. The number of in-sync replicas cannot be the same as the number of replicas of the topic. Otherwise, if one replica is unavailable, messages cannot be produced.

You can enable or disable automatic topic creation. Enabling this function automatically creates a topic when a message is produced in or consumed from a topic that does not exist.

Others
------

Maximum number of connections: 3000

Maximum size of a message: 10 MB

Access Kafka using SASL_SSL. Ensure that your DNS service is capable of resolving an IP address to a domain name. Alternatively, map all Kafka broker IP addresses to host names in the **hosts** file. Prevent Kafka clients from performing reverse resolution. Otherwise, connections may fail to be established.

Apply for a disk space size that is more than twice the size of service data multiplied by the number of replicas. In other words, keep 50% of the disk space idle.

Avoid frequent full GC in JVM. Otherwise, message production and consumption will be blocked.
