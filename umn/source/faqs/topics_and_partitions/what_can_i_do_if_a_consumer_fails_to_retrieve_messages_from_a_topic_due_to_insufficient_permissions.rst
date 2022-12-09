:original_name: kafka-faq-0038.html

.. _kafka-faq-0038:

What Can I Do If a Consumer Fails to Retrieve Messages from a Topic Due to Insufficient Permissions?
====================================================================================================

**Symptom**: Different consumers in a consumer group have different topic permissions. When a consumer attempts to retrieve messages from a topic, the error message "Not authorized to access topics." is displayed, and the message retrieval fails.

|image1|

**Analysis**: When assigning partitions, the leader of the consumer group does not consider the permissions of individual consumers. Instead, the leader assigns partitions based on the overall subscription of the consumer group. In this case, consumers may be assigned topics that they do not have access to.

For example, consumers A, B, and C are in the same consumer group. Consumer A has subscribed to and has permissions to access Topics 0, 1, and 2; consumer B has subscribed to and has permissions to access Topics 3, 4, and 5; consumer C has subscribed to and has permissions to access Topics 6, 7, and 8. Assume that each topic has only one partition. Based on the partition assignment determined by the leader, consumer A may be assigned Topics 0, 3, and 6; consumer B is assigned Topics 1, 4, and 7; and consumer C is assigned Topics 2, 5, and 8. In this case, consumer A does not have permissions to access Topics 3 and 6, resulting in the error.


.. figure:: /_static/images/en-us_image_0000001384665714.png
   :alt: **Figure 1** Consumer access permissions

   **Figure 1** Consumer access permissions

**Solution:**

-  If all consumers must be in the same consumer group (**group.id** is the same), grant the same topic access permissions to all the consumers.
-  If the consumers do not need to be in the same consumer group, change the value of **group.id** to ensure that each consumer is in a separate consumer group.

.. |image1| image:: /_static/images/en-us_image_0000001098967408.png
