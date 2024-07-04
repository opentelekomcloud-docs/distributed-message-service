:original_name: kafka_faq_0056.html

.. _kafka_faq_0056:

Why Does Message Production Fail During Scaling?
================================================

**Possible cause**: When you increase the broker flavor, a rolling restart is performed on brokers. During the restart, partition leaders are changed. The producer has cached the old partition leader IDs, so messages are still sent to old partition leaders. As a result, messages fail to be produced.

**Solution**: Configure the retry mechanism on the producer by setting **retries** to **Integer.MAX_VALUE**.
