:original_name: how-to-connect-kafka.html

.. _how-to-connect-kafka:

Setting Up the Java Development Environment
===========================================

With the information collected in :ref:`Collecting Connection Information <kafka-config>` and the network environment prepared for Kafka clients, you can proceed to configuring Kafka clients. This section describes how to configure Kafka clients to produce and consume messages.

Preparing Tools
---------------

-  Maven

   Apache Maven 3.0.3 or later can be downloaded from the `Maven official website <https://maven.apache.org/download.cgi>`__.

-  JDK

   Java Development Kit1.8.111 or later can be downloaded from the `Oracle official website <https://www.oracle.com/technetwork/java/javase/downloads/index.html>`__.

   After the installation, configure the Java environment variables.

-  IntelliJ IDEA

   IntelliJ IDEA can be downloaded from the `IntelliJ IDEA official website <https://www.jetbrains.com/idea/>`__ and be installed.

Procedure
---------

#. `Download the demo package <https://dms-demo.obs.eu-de.otc.t-systems.com/Kafka-sdk-java.zip>`__.

   Decompress the package to obtain the following files.

   .. table:: **Table 1** Files in the demo package

      +-----------------------------+----------------------------------------+--------------------------------------------------------------------+
      | File                        | Directory                              | Description                                                        |
      +=============================+========================================+====================================================================+
      | DmsConsumer.java            | .\\src\\main\\java\\com\\dms\\consumer | API for consuming messages                                         |
      +-----------------------------+----------------------------------------+--------------------------------------------------------------------+
      | DmsProducer.java            | .\\src\\main\\java\\com\\dms\\producer | API for producing messages                                         |
      +-----------------------------+----------------------------------------+--------------------------------------------------------------------+
      | dms.sdk.consumer.properties | .\\src\\main\\resources                | Configuration information for consuming messages                   |
      +-----------------------------+----------------------------------------+--------------------------------------------------------------------+
      | dms.sdk.producer.properties | .\\src\\main\\resources                | Configuration information for producing messages                   |
      +-----------------------------+----------------------------------------+--------------------------------------------------------------------+
      | client.jks                  | .\\src\\main\\resources                | SSL certificate, used for SASL_SSL connection                      |
      +-----------------------------+----------------------------------------+--------------------------------------------------------------------+
      | DmsConsumerTest.java        | .\\src\\test\\java\\com\\dms\\consumer | Test code of consuming messages                                    |
      +-----------------------------+----------------------------------------+--------------------------------------------------------------------+
      | DmsProducerTest.java        | .\\src\\test\\java\\com\\dms\\producer | Test code of producing messages                                    |
      +-----------------------------+----------------------------------------+--------------------------------------------------------------------+
      | pom.xml                     | .\\                                    | Maven configuration file, containing the Kafka client dependencies |
      +-----------------------------+----------------------------------------+--------------------------------------------------------------------+

#. In IntelliJ IDEA, import the demo project.

   The demo project is a Java project built in Maven. Therefore, you need the JDK and the Maven plugin in IDEA.


   .. figure:: /_static/images/en-us_image_0171660980.png
      :alt: **Figure 1** Click **Import Project**.

      **Figure 1** Click **Import Project**.


   .. figure:: /_static/images/en-us_image_0171660966.png
      :alt: **Figure 2** Choose **Maven**.

      **Figure 2** Choose **Maven**.


   .. figure:: /_static/images/en-us_image_0171660975.png
      :alt: **Figure 3** Select the JDK.

      **Figure 3** Select the JDK.

   You can select other options or retain the default settings. Click **Finish**.

   The demo project has been imported.

   |image1|

#. Configure Maven.

   Choose **Files** > **Settings**, set **Maven home directory** correctly, and select the required **settings.xml** file.

   |image2|

#. Specify Kafka configurations.

   This section uses the example of producing messages. For details, see :ref:`Producer configuration file <kafka-java-demo__li106711612652>`.

#. In the down left corner of IDEA, click **Terminal**. In terminal, run the **mvn test** command to see how the demo project goes.


   .. figure:: /_static/images/en-us_image_0171660984.png
      :alt: **Figure 4** Opening terminal in IDEA

      **Figure 4** Opening terminal in IDEA

   The following information is displayed for the producer:

   .. code-block::

      -------------------------------------------------------
       T E S T S
      -------------------------------------------------------
      Running com.dms.producer.DmsProducerTest
      produce msg:The msg is 0
      produce msg:The msg is 1
      produce msg:The msg is 2
      produce msg:The msg is 3
      produce msg:The msg is 4
      produce msg:The msg is 5
      produce msg:The msg is 6
      produce msg:The msg is 7
      produce msg:The msg is 8
      produce msg:The msg is 9
      Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 138.877 sec

   The following information is displayed for the consumer:

   .. code-block::

      -------------------------------------------------------
       T E S T S
      -------------------------------------------------------
      Running com.dms.consumer.DmsConsumerTest
      the numbers of topic:0
      the numbers of topic:0
      the numbers of topic:6
      ConsumerRecord(topic = topic-0, partition = 2, offset = 0, CreateTime = 1557059377179, serialized key size = -1, serialized value size = 12, headers = RecordHeaders(headers = [], isReadOnly = false), key = null, value = The msg is 2)
      ConsumerRecord(topic = topic-0, partition = 2, offset = 1, CreateTime = 1557059377195, serialized key size = -1, serialized value size = 12, headers = RecordHeaders(headers = [], isReadOnly = false), key = null, value = The msg is 5)

.. |image1| image:: /_static/images/en-us_image_0171660939.png
.. |image2| image:: /_static/images/en-us_image_0171660970.png
