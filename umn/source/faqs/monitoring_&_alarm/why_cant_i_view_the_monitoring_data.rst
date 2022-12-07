:original_name: kafka-faq-200426041.html

.. _kafka-faq-200426041:

Why Can't I View the Monitoring Data?
=====================================

The possible causes are as follows:

-  The topic name starts with a special character, such as an underscore (_) or a number sign (#).
-  The consumer group name starts with a special character, such as an underscore (_) or a number sign (#).

To solve the problem, delete topics and consumer groups whose names contain the special character.
