:original_name: kafka-faq-200426036.html

.. _kafka-faq-200426036:

Why Does Message Poll Often Fail During Rebalancing?
====================================================

Rebalancing is a process where partitions of topics are re-allocated for a consumer group.

In normal cases, rebalancing occurs inevitably when a consumer is added to or removed from a consumer group. However, if a consumer is regarded as abnormal by the server and removed from the consumer group, message consumption may fail.

This may happen in the following scenarios:

#. Heartbeat requests are not sent in time.

   A consumer sends heartbeat requests to the broker at the interval specified by **heartbeat.interval.ms**. If the broker does not receive any heartbeat request from the consumer within the period specified by **session.timeout.ms**, the broker considers that the consumer is abnormal and removes the consumer from the consumer group, triggering rebalancing.

#. The interval between retrievals is too long.

   The maximum number of messages that a consumer can consume at a time is specified by **max.poll.records**. In most cases, a client processes the consumed data before starting the next consumption. The processing may be prolonged when a large number of messages are consumed at a time and cannot be processed within the time specified by **max.poll.interval.ms**, or when an exception occurs during the process (for example, data needs to be written to the backend database, but the backend database pressure is too high, resulting in slow SQL and high latency). If the consumer does not send the next consumption request within the time specified by **max.poll.interval.ms**, the broker considers that the consumer is inactive and removes it from the consumer group, triggering rebalancing.

Solutions and Troubleshooting Methods
-------------------------------------

**Scenario 1:** Heartbeat requests are not sent in time.

**Locating:** If the client is in Java, check GC logs to see whether FullGC takes a long time. If yes, the heartbeat thread may be blocked. As a result, the server fails to check heartbeats and starts rebalancing.

**Solution:** Check for client issues. FullGC indicates that memory leakage may have occurred on the client.

**Scenario 2:** The interval between retrievals is too long.

**Troubleshooting methods:**

#. Check the time required for processing a single message and whether the time required for processing a specified number (**max.poll.records**) of messages exceeds the time specified by **max.poll.interval.ms**.
#. Check whether message processing requires network connections, such as writing data to the database and calling backend APIs, and whether the downstream consumer system is normal in rebalancing scenarios.

**Solution**: On the consumer client, decrease the value of **max.poll.records**. If message processing takes longer, increase the value of **max.poll.interval.ms**.
