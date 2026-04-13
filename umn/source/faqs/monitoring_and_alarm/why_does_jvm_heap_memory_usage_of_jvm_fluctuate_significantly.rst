:original_name: kafka-faq-0064.html

.. _kafka-faq-0064:

Why Does JVM Heap Memory Usage of JVM Fluctuate Significantly?
==============================================================

It is normal that **JVM Heap Memory Usage of JVM** is displayed in a sawtooth shape on the monitoring page. The maximum value may further increase or the fluctuation may be greater after scale-out or an engine upgrade. Such fluctuations are caused by normal JVM heap memory reclamation, and do not affect services.
