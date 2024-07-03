:original_name: kafka-faq-200426012.html

.. _kafka-faq-200426012:

How Long Are Kafka SSL Certificates Valid for?
==============================================

The certificates are valid for more than 15 years. You do not need to worry about certificate expiration. The certificates are used for one-way authentication when enabling SASL_SSL for Kafka instances.

To check the validity of the SSL certificate, perform the following steps:

#. Decompress the package downloaded from the Kafka instance console to obtain **phy_ca.crt**.

#. Double-click **phy_ca.crt**. The **Certificate** dialog box is displayed.

#. On the **General** tab page, view the certificate validity period.


   .. figure:: /_static/images/en-us_image_0000001586445178.png
      :alt: **Figure 1** Certificate validity period

      **Figure 1** Certificate validity period
