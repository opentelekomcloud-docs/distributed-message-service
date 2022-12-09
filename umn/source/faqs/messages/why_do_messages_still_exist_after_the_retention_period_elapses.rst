:original_name: kafka-faq-200708001.html

.. _kafka-faq-200708001:

Why Do Messages Still Exist After the Retention Period Elapses?
===============================================================

If the aging time has been set for a topic, the value of the **log.retention.hours** parameter does not take effect for the topic. The value of the **log.retention.hours** parameter takes effect only if the aging time has not been set for the topic.

**Possible cause 1:** The segment files are in use.

**Solution:** Wait until the segment is no longer in use or delete the topic where messages have reached their retention period.

**Possible cause 2**: In a topic, there is a message whose **CreateTime** is a future time. For example, assume that it is January 1, and the **CreateTime** is February 1. The message will not be aged after 72 hours from now. As a result, messages created subsequently will also not be aged.

**Solution**: Delete the topic where the **CreateTime** of a message is a future time.
