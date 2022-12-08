:original_name: kafka-faq-200426028.html

.. _kafka-faq-200426028:

Why Do Deleted Topics Still Exist?
==================================

This may be because automatic topic creation has been enabled and a consumer is connecting to the topic. If no existing topics are available for message creation, new topics will be automatically created.

To solve this problem, disable automatic topic creation.
