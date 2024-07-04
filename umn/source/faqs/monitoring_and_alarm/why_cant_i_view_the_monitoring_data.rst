:original_name: kafka-faq-200426041.html

.. _kafka-faq-200426041:

Why Can't I View the Monitoring Data?
=====================================

If topic monitoring data is not displayed, the possible causes are as follows:

-  The topic name starts with a special character, such as an underscore (_) or a number sign (#).
-  No topic is created in the Kafka instance.

Solution:

-  Delete topics whose names contain special characters.
-  Create a topic.

If consumer group monitoring data is not displayed, the possible causes are as follows:

-  The consumer group name starts with a special character, such as an underscore (_) or a number sign (#).
-  No consumers in the group have connected to the instance.

Solution:

-  Delete consumer groups whose names contain special characters.
-  Consume messages using this consumer group.
