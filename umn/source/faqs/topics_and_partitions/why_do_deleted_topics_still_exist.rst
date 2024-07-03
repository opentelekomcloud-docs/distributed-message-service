:original_name: kafka-faq-200426028.html

.. _kafka-faq-200426028:

Why Do Deleted Topics Still Exist?
==================================

**Possible cause**: Automatic topic creation has been enabled and a consumer is connecting to the topic. If no existing topics are available for message creation, new topics will be automatically created.

**Solution**: Disable automatic topic creation.
