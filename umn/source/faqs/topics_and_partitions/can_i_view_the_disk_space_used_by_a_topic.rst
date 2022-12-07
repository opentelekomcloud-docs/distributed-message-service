:original_name: kafka-faq-200426030.html

.. _kafka-faq-200426030:

Can I View the Disk Space Used by a Topic?
==========================================

Yes. Use either of the following methods to check the disk space used by a topic:

-  Click |image1| next to the Kafka instance name to go to the Cloud Eye console. On the **Queues** tab page, set **Queue** to the name of the topic whose disk space you want to view and **Scope** to **Basic monitoring**. The **Message Size** metric reflects the message size of the selected topic.
-  Click the desired Kafka instance to view its details. In the navigation pane, choose **Monitoring**. On the **By Topic** tab page, set **Topic** to the name of the topic whose disk space you want to view and **Monitoring Type** to **Basic monitoring**. The **Message Size** metric reflects the message size of the selected topic.

.. |image1| image:: /_static/images/en-us_image_0000001381108612.png
