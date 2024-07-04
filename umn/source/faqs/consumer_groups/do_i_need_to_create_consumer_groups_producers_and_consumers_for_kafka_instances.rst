:original_name: kafka-faq-200426033.html

.. _kafka-faq-200426033:

Do I Need to Create Consumer Groups, Producers, and Consumers for Kafka Instances?
==================================================================================

-  When parameter **auto.create.groups.enable** is set to **true**, you do not need to create a consumer group, producer, or consumer because they are generated automatically when you use the instance.
-  When parameter **auto.create.groups.enable** is set to **false**, you need to create a consumer group, but do not need to create a producer or consumer.

To change the **auto.create.groups.enable** setting, see :ref:`Modifying Kafka Instance Configuration Parameters <kafka-ug-0007>`.

For details about producing and consuming messages after connecting to a Kafka instance, see :ref:`Connecting to Kafka Using the Client (Plaintext Access) <kafka-ug190605003>`.
