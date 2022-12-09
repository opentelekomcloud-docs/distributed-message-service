:original_name: Kafka-client-optimize.html

.. _Kafka-client-optimize:

Recommendations on Client Usage
===============================

-  Producer parameters

   -  Allow for retries in cases where messages fail to be sent.

      For example, allow for three retries by setting the value of **retries** to **3**.

   -  The producer cannot block on callback functions. Otherwise, messages may fail to be sent.

      For messages that need to be send immediately, set **linger.ms** to **0**.

      Ensure that the producer has sufficient JVM memory to avoid blockages.

-  Consumer parameters

   -  Ensure that the owner thread does not exit abnormally. Otherwise, the client may fail to initiate consumption requests and the consumption will be blocked.
   -  Use long polling to consume messages and do not close the consumer connection immediately after the consumption is completed. Otherwise, rebalancing will take place frequently, blocking consumption.
   -  Ensure that the consumer polls at regular intervals (for example, every 200 ms) for it to keep sending heartbeats to the server. If the consumer stops sending heartbeats for long enough, the consumer session will time out and the consumer will be considered to have stopped. This will also block consumption.
   -  Always close the consumer before exiting. Otherwise, consumers in the same group may block the **session.timeout.ms** time.
   -  Set the timeout time for the consumer session to a reasonable value. For example, set **session.timeout.ms** to **30000** so that the timeout time is 30s.
   -  The number of consumers cannot be greater than the number of partitions in the topic. Otherwise, some consumers may fail to poll for messages.
   -  Commit messages after they have been processed. Otherwise, the messages may fail to be processed and cannot be polled for again.
   -  Ensure that there is a maximum limit on the size of messages buffered locally to avoid an out-of-memory (OOM) situation.
   -  Kafka supports the exactly-once delivery. Therefore, ensure the idempotency of processing messages for services.
