:original_name: kafka-ug-180604014.html

.. _kafka-ug-180604014:

Viewing and Modifying Basic Information of a Kafka Instance
===========================================================

After creating a Kafka instance, you can view the details or modify some parameters of it on the console as required. These parameters include the instance name, description, security group, and capacity threshold policy.

.. note::

   Single-node instances do not support reconfiguration of Smart Connect and private network access.

Prerequisite
------------

You can modify basic information of a Kafka instance when the instance is in the **Running** state.

Viewing Kafka Instance Details
------------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. You can filter Kafka instances by tag, status, name, version, flavor, used/available storage space, maximum partitions, billing mode, and enterprise project. Only enterprise users can filter instances by enterprise projects. For Kafka instance statuses, see :ref:`Table 1 <kafka-ug-180604014__table5086721717534>`.

   .. _kafka-ug-180604014__table5086721717534:

   .. table:: **Table 1** Kafka instance status description

      +-----------------------------------+-------------------------------------------------------------------------------------------------------------+
      | Status                            | Description                                                                                                 |
      +===================================+=============================================================================================================+
      | Creating                          | The instance is being created.                                                                              |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------+
      | Creation failed                   | The instance failed to be created.                                                                          |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------+
      | Running                           | The instance is running properly.                                                                           |
      |                                   |                                                                                                             |
      |                                   | Only instances in the **Running** state can provide services.                                               |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------+
      | Faulty                            | The instance is not running properly.                                                                       |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------+
      | Restarting                        | The instance is being restarted.                                                                            |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------+
      | Changing                          | The instance specifications or public access configurations are being modified.                             |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------+
      | Change failed                     | The instance specifications or public access configurations failed to be modified.                          |
      |                                   |                                                                                                             |
      |                                   | You cannot restart, delete, or modify an instance in the **Change failed** state. Contact customer service. |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------+

#. Click the name of the desired Kafka instance and view detailed information about the instance on the **Basic Information** tab page.

   :ref:`Table 2 <kafka-ug-180604014__table172443431061>` describes the parameters for connecting to a Kafka instance. For details about other parameters, see the **Basic Information** tab page of the Kafka instance on the console.

   .. _kafka-ug-180604014__table172443431061:

   .. table:: **Table 2** Connection parameters

      +-----------------+------------------------+---------------------------------------+--------------------------------------------------------------------------------+
      | Section         | Parameter              | Sub-Parameter                         | Description                                                                    |
      +=================+========================+=======================================+================================================================================+
      | Connection      | Username               | ``-``                                 | Username for accessing the instance with ciphertext access enabled.            |
      +-----------------+------------------------+---------------------------------------+--------------------------------------------------------------------------------+
      |                 | Private Network Access | Plaintext Access                      | Indicates whether plaintext access is enabled.                                 |
      +-----------------+------------------------+---------------------------------------+--------------------------------------------------------------------------------+
      |                 |                        | Address (Private Network, Plaintext)  | This parameter is displayed only after you enable **Plaintext Access**.        |
      +-----------------+------------------------+---------------------------------------+--------------------------------------------------------------------------------+
      |                 |                        | Ciphertext Access                     | Indicates whether ciphertext access is enabled.                                |
      |                 |                        |                                       |                                                                                |
      |                 |                        |                                       | This function is unavailable for single-node instances.                        |
      +-----------------+------------------------+---------------------------------------+--------------------------------------------------------------------------------+
      |                 |                        | Address (Private Network, Ciphertext) | This parameter is displayed only after you enable **Ciphertext Access**.       |
      +-----------------+------------------------+---------------------------------------+--------------------------------------------------------------------------------+
      |                 |                        | Security Protocol                     | This parameter is displayed only after you enable **Ciphertext Access**.       |
      +-----------------+------------------------+---------------------------------------+--------------------------------------------------------------------------------+
      |                 | Public Network Access  | Toggle switch                         | Indicates whether public access has been enabled.                              |
      +-----------------+------------------------+---------------------------------------+--------------------------------------------------------------------------------+
      |                 |                        | Plaintext Access                      | This parameter is displayed only when **Public Access** is enabled.            |
      |                 |                        |                                       |                                                                                |
      |                 |                        |                                       | Indicates whether plaintext access is enabled.                                 |
      +-----------------+------------------------+---------------------------------------+--------------------------------------------------------------------------------+
      |                 |                        | Address (Public Network, Plaintext)   | This parameter is displayed only after you enable **Plaintext Access**.        |
      +-----------------+------------------------+---------------------------------------+--------------------------------------------------------------------------------+
      |                 |                        | Ciphertext Access                     | This parameter is displayed only when **Public Access** is enabled.            |
      |                 |                        |                                       |                                                                                |
      |                 |                        |                                       | Indicates whether ciphertext access is enabled.                                |
      |                 |                        |                                       |                                                                                |
      |                 |                        |                                       | This function is unavailable for single-node instances.                        |
      +-----------------+------------------------+---------------------------------------+--------------------------------------------------------------------------------+
      |                 |                        | Address (Public Network, Ciphertext)  | This parameter is displayed only after you enable **Ciphertext Access**.       |
      +-----------------+------------------------+---------------------------------------+--------------------------------------------------------------------------------+
      |                 |                        | Security Protocol                     | This parameter is displayed only after you enable **Ciphertext Access**.       |
      +-----------------+------------------------+---------------------------------------+--------------------------------------------------------------------------------+
      |                 | SASL Mechanism         | ``-``                                 | This parameter is displayed only after you enable **Ciphertext Access**.       |
      +-----------------+------------------------+---------------------------------------+--------------------------------------------------------------------------------+
      |                 | SSL Certificate        | ``-``                                 | This parameter is displayed only when SASL_SSL is enabled.                     |
      |                 |                        |                                       |                                                                                |
      |                 |                        |                                       | Click **Download** to download the SSL certificate for accessing the instance. |
      +-----------------+------------------------+---------------------------------------+--------------------------------------------------------------------------------+

Modifying Basic Information of a Kafka Instance
-----------------------------------------------

#. Log in to the console.
#. Click |image2| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired Kafka instance to view its details.
#. Modify the following parameters if needed:

   .. table:: **Table 3** Modifiable Kafka parameters

      +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+
      | Parameter                 | How to Modify                                                                                                                                       | Result                                                                                                        |
      +===========================+=====================================================================================================================================================+===============================================================================================================+
      | Instance Name             | Click |image3|, enter a new name, and click |image4|.                                                                                               | The modification result is displayed in the upper right corner of the page.                                   |
      |                           |                                                                                                                                                     |                                                                                                               |
      |                           | Naming rules: 4-64 characters; starts with a letter; can contain only letters, digits, hyphens (-), and underscores (_).                            |                                                                                                               |
      +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+
      | Enterprise Project        | Click |image5|, select a new enterprise project from the drop-down list, and click |image6|.                                                        | The modification result is displayed in the upper right corner of the page.                                   |
      |                           |                                                                                                                                                     |                                                                                                               |
      |                           | Only for enterprise users. Modifying this parameter does not restart the instance.                                                                  |                                                                                                               |
      +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+
      | Description               | Click |image7|, enter a new description, and click |image8|.                                                                                        | The modification result is displayed in the upper right corner of the page.                                   |
      |                           |                                                                                                                                                     |                                                                                                               |
      |                           | 0 to 1024 characters.                                                                                                                               |                                                                                                               |
      +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+
      | Security Group            | Click |image9|, select a new security group from the drop-down list, and click |image10|.                                                           | The modification result is displayed in the upper right corner of the page.                                   |
      |                           |                                                                                                                                                     |                                                                                                               |
      |                           | Modifying this parameter does not restart the instance.                                                                                             |                                                                                                               |
      +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+
      | Private Network Access    | See :ref:`Configuring Plaintext or Ciphertext Access to Kafka Instances <kafka_ug_0044>`.                                                           | You will be redirected to the **Background Tasks** page, which displays the modification progress and result. |
      +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+
      | Public Access             | See :ref:`Configuring Kafka Public Access <kafka-ug-0319001>`.                                                                                      | You will be redirected to the **Background Tasks** page, which displays the modification progress and result. |
      +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+
      | Capacity Threshold Policy | Click the desired policy. In the displayed **Confirm** dialog box, click **OK**.                                                                    | You will be redirected to the **Background Tasks** page, which displays the modification progress and result. |
      |                           |                                                                                                                                                     |                                                                                                               |
      |                           | Modifying this parameter does not restart the instance.                                                                                             |                                                                                                               |
      +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+
      | Automatic Topic Creation  | Enable/Disable this **Automatic Topic Creation**. In the displayed **Confirm** dialog box, click **OK**.                                            | You will be redirected to the **Background Tasks** page, which displays the modification progress and result. |
      |                           |                                                                                                                                                     |                                                                                                               |
      |                           | Changing this option may restart the instance.                                                                                                      |                                                                                                               |
      +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+
      | Cross-VPC Access          | See :ref:`Accessing Kafka Using a VPC Endpoint Across VPCs <kafka-ug-0001>` and :ref:`Accessing Kafka in a Public Network Using DNAT <kafka-dnat>`. | The modification result is displayed in the upper right corner of the page.                                   |
      +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0143929918.png
.. |image3| image:: /_static/images/en-us_image_0000001093972624.png
.. |image4| image:: /_static/images/en-us_image_0000001191769789.png
.. |image5| image:: /_static/images/en-us_image_0000001093972624.png
.. |image6| image:: /_static/images/en-us_image_0000001191769789.png
.. |image7| image:: /_static/images/en-us_image_0000001093972624.png
.. |image8| image:: /_static/images/en-us_image_0000001191769789.png
.. |image9| image:: /_static/images/en-us_image_0000001093972624.png
.. |image10| image:: /_static/images/en-us_image_0000001191769789.png
