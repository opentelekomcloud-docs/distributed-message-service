:original_name: kafka-faq-200426013.html

.. _kafka-faq-200426013:

How Do I Synchronize Data from One Kafka Instance to Another?
=============================================================

Unfortunately, you cannot synchronize two Kafka instances in real time. To migrate services from one instance to another, create messages to both instances. After all messages in the original instance have been retrieved or aged, you can migrate services to the new instance.
