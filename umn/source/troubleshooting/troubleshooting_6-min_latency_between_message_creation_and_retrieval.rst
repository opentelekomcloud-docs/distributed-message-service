:original_name: kafka-trouble-0709001.html

.. _kafka-trouble-0709001:

Troubleshooting 6-Min Latency Between Message Creation and Retrieval
====================================================================

Symptom
-------

**The duration from message creation to retrieval occasionally reaches 6 minutes**, which is not tolerable to services.

Possible Causes
---------------

#. Service requests are stacked and cannot be processed in time.

   According to the monitoring data, only up to 50 messages are stacked and up to 10 messages are created per second, which is within the processing capability limit, so this is not the cause of the symptom.

#. The EIP inbound traffic decreases.

   If the EIP technical support personnel cannot find any problem, this is not the cause of the symptom.

#. The consumer group is behaving abnormally.

   According to the server logs, the consumer group is going through frequent rebalance operations. While most rebalance operations are completed within seconds, some can take several minutes. Messages cannot be retrieved until the rebalance is complete.

   This is the cause of the symptom.

Detailed Analysis
-----------------

A consumer group may exhibit the following three types of behavior in the log:

-  **Preparing to rebalance group 1**

   The consumer group starts rebalance, and its status changes to **REABLANCING**.

-  **Stabilized group**

   The consumer group completes rebalance, and its status changes to **STABILIZED**.

-  **Member consumer-xxx in group 1 has failed**

   A consumer in a consumer group leaves the group if **the consumer has not communicated with the server for a long time**. This is usually triggered if the message processing is prolonged and the process is blocked.

The following figure shows the duration between **Preparing** and **Stabilized**. **The time shown in the figure is UTC+0.**


.. figure:: /_static/images/en-us_image_0000001073862086.png
   :alt: **Figure 1** Consumer group rebalance

   **Figure 1** Consumer group rebalance

This set of data shows that rebalance performance of the consumer group deteriorates after 06:49 on July 1. As a result, the client becomes abnormal.

Root Cause
----------

Sometimes, **a consumer cannot respond to rebalancing in a timely manner. As a result, the entire consumer group is blocked** until the consumer responds.

Workaround
----------

#. Use different consumer groups for different services to reduce the impact of a single consumer blocking access.
#. **max.poll.interval.ms** sets the maximum interval for a consumer group to request message consumption. If a consumer does not initiate another consumption request before timeout, the server triggers rebalancing. You can increase the default value of **max.poll.interval.ms**.

Solution
--------

#. Use different consumer groups for different services.
#. Optimize the service processing logic to improve the processing efficiency and reduce the blocking time.

Background Knowledge
--------------------

A consumer group can be either **REBALANCING** or **STABILIZED**.

-  **REBALANCING**: If a consumer joins or leaves a consumer group, the metadata of the consumer group changes and **no consumers in the consumer group can retrieve messages**.
-  **STABILIZED**: The metadata has been synchronized by all consumers in the consumer group, including existing ones. Rebalancing has completed and the consumer group is stabilized. Consumers in the consumer group **can retrieve messages normally**.

A consumer group works as follows:

#. A consumer leaves or joins the group, changing the consumer group metadata recorded at the server. The server updates the consumer group status to **REBALANCING**.
#. The server **waits for all consumers** (including existing ones) to synchronize the latest metadata.
#. After **all consumers** have synchronized the latest metadata, the server updates the consumer group status to **STABILIZED**.
#. Consumers retrieve messages.
