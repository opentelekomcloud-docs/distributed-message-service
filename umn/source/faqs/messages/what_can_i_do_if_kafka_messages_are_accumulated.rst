:original_name: kafka-faq-200426100.html

.. _kafka-faq-200426100:

What Can I Do If Kafka Messages Are Accumulated?
================================================

**Symptom**: An alarm is generated for the **Accumulated Messages** metric.

**Solution:**

#. Log in to the Kafka console and click the instance for which the alarm is generated. The instance details page is displayed.
#. Choose **Monitoring** in the navigation pane.
#. On the **By Consumer Group** tab page, view **Consumer Available Messages** to find the consumer group with accumulated messages.
#. In the navigation pane, choose **Consumer Groups**.
#. Check whether there are consumers in the consumer group where messages are accumulated. If yes, contact the service party to accelerate their consumption. If no, contact the customer to delete unused consumer groups.
