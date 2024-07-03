:original_name: kafka-pd-190605002.html

.. _kafka-pd-190605002:

Related Services
================

-  Cloud Trace Service (CTS)

   CTS generates traces to provide you with a history of operations performed on cloud service resources. The traces include operation requests sent using the management console or open APIs, as well as the operation results. You can view all generated traces to query, audit, and backtrack performed operations.

   For details about the operations recorded by CTS, see :ref:`Operations Logged by CTS <kafka-ug-180418002>`.

-  Virtual Private Cloud (VPC)

   Kafka instances run in VPCs and use the IP addresses and bandwidth of VPC. Security groups of VPCs enhance the security of network access to the Kafka instances.

-  Elastic Cloud Server (ECS)

   An ECS is a basic computing unit that consists of vCPUs, memory, OS, and EVS disks. Kafka instances run on ECSs. A broker corresponds to an ECS.

-  Elastic Volume Service (EVS)

   EVS provides block storage services for ECSs. All Kafka data, such as messages, metadata, and logs, is stored in EVS disks.

-  Identity and Access Management (IAM)

   IAM enables you to easily manage users and control their access to cloud services and resources. Grant different users different Kafka permissions required to perform a given task based on their job responsibilities.

-  Cloud Eye (CES)

   Cloud Eye is an open platform that provides monitoring, alarm reporting, and alarm notification for your resources in real time.

   For details about DMS metrics monitored by Cloud Eye, see :ref:`Kafka Metrics <kafka-ug-180413002>`.

   .. note::

      The values of all Kafka instance metrics are reported to Cloud Eye every minute.

-  Elastic IP (EIP)

   The EIP service provides independent public IP addresses and bandwidth for Internet access. Kafka instances bound with EIPs can be accessed over public networks.

-  Tag Management Service (TMS)

   TMS is a visualized service for fast and unified cross-region tagging and categorization of cloud services.

   Tags facilitate Kafka instance identification and management.

-  Key Management Service (KMS)

   When creating a Kafka instance, you can specify whether to enable disk encryption. Enabling disk encryption improves data security. Disk encryption depends on the keys provided by KMS.
