:original_name: kafka-faq-200426036.html

.. _kafka-faq-200426036:

Why Does Message Poll Often Fail During Rebalancing?
====================================================

Rebalancing is a process where partitions of topics are re-allocated for a consumer group.

In normal cases, rebalancing occurs inevitably when a consumer is added to or removed from a consumer group. However, if a consumer is regarded as abnormal and removed from the consumer group, message retrieval may fail.

This may happen in the following scenarios:

#. Heartbeat requests are not sent in time.

   A consumer sends heartbeat requests to the broker at the interval specified by **heartbeat.interval.ms**. If the broker does not receive any heartbeat request from the consumer within the period specified by **session.timeout.ms**, the broker considers that the consumer is abnormal and removes the consumer from the consumer group, triggering rebalancing.

#. The interval between retrievals is too long.

   The maximum number of messages that a consumer can retrieve at a time is specified by **max.poll.records**. In most cases, a client processes the retrieved data before starting the next retrieval. The processing may be prolonged when a large number of messages are retrieved at a time and cannot be processed within the time specified by **max.poll.interval.ms**, or when an exception occurs during the process (for example, data needs to be written to the backend database, but the backend database pressure is too high, resulting in high latency). If the consumer does not send the next retrieval request within the time specified by **max.poll.interval.ms**, the broker considers that the consumer is inactive and removes it from the consumer group, triggering rebalancing.

Solutions and Troubleshooting Methods
-------------------------------------

**Scenario 1:** Heartbeat requests are not sent in time.

**Solution**: Set the value of **session.timeout.ms** to three times the value of **heartbeat.interval.ms**.

**Scenario 2:** The interval between retrievals is too long.

**Troubleshooting methods:**

#. Check the time required for processing a single message and whether the time required for processing a specified number (**max.poll.records**) of messages exceeds the time specified by **max.poll.interval.ms**.
#. Check whether message processing requires network connections, such as writing data to the database and calling backend APIs, and whether the backend is normal in rebalancing scenarios.
