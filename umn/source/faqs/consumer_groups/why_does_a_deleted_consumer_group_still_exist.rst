:original_name: kafka_faq_0059.html

.. _kafka_faq_0059:

Why Does a Deleted Consumer Group Still Exist?
==============================================

**Possible cause**: Automatic consumer group creation has been enabled and your service is connected to the consumer group and consuming messages. Therefore, the consumer group is deleted but will be automatically re-created to consume messages until your service stops.

**Solution**: Disable automatic consumer group creation. To do so, go to the Kafka console, choose **Parameters** in the left navigation pane, locate the row that contains **auto.create.groups.enable** in the **Dynamic Parameters** area, click **Edit**, set the **Current Value** to **false**, and click **Save**. Then, delete the consumer group. **auto.create.groups.enable** is not displayed for some instances. For details, see the console. In this case, modify your service code to stop connecting to the consumer group. Then, delete the consumer group. For details about how to modify **auto.create.groups.enable**, see :ref:`Modifying Kafka Instance Configuration Parameters <kafka-ug-0007>`.
