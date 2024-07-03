:original_name: CreateUserAndGrantPolicy.html

.. _CreateUserAndGrantPolicy:

Creating a User and Granting DMS for Kafka Permissions
======================================================

This section describes how to use `Identity and Access Management (IAM) <https://docs.otc.t-systems.com/en-us/usermanual/iam/iam_01_0026.html>`__ for fine-grained permissions control for your Distributed Message Service (DMS) for Kafka resources. With IAM, you can:

-  Create IAM users for personnel based on your enterprise's organizational structure. Each IAM user has their own identity credentials for accessing DMS for Kafka resources.
-  Grant users only the permissions required to perform a given task based on their job responsibilities.
-  Entrust another account or cloud service to perform efficient O&M on your DMS for Kafka resources.

If your account meets your permissions requirements, you can skip this section.

This section describes the procedure for granting permissions (see :ref:`Figure 1 <createuserandgrantpolicy__fig207161552102018>`).

Prerequisites
-------------

Learn about the permissions (see System-defined roles and policies supported by DMS for Kafka) supported by DMS for Kafka and choose policies according to your requirements. For the permissions of other services, see `Permissions <https://docs.otc.t-systems.com/en-us/permissions/index.html>`__.

Process Flow
------------

.. _createuserandgrantpolicy__fig207161552102018:

.. figure:: /_static/images/en-us_image_0000001284017553.png
   :alt: **Figure 1** Process for granting DMS for Kafka permissions

   **Figure 1** Process for granting DMS for Kafka permissions

#. For the following example, `create a user group on the IAM console <https://docs.otc.t-systems.com/en-us/usermanual/iam/iam_01_0030.html>`__ and assign the **DMS ReadOnlyAccess** policy to the group.

#. `Create an IAM user and add it to the created user group <https://docs.otc.t-systems.com/en-us/usermanual/iam/iam_01_0031.html>`__.

#. `Log in as the IAM user <https://docs.otc.t-systems.com/en-us/usermanual/iam/iam_01_0032.html>`__ and verify permissions.

   In the authorized region, perform the following operations:

   -  Choose **Service List** > **Distributed Message Service**. Then click **Create Instance** on the console of DMS for Kafka. If a message appears indicating that you cannot perform the operation, the **DMS ReadOnlyAccess** policy is in effect.
   -  Choose **Service List** > **Elastic Volume Service**. If a message appears indicating that you have insufficient permissions, the **DMS ReadOnlyAccess** policy is in effect.
   -  Choose **Service List** > Distributed Message Service. If the Kafka instance list can be displayed, the **DMS ReadOnlyAccess** policy is in effect.

Example Custom Policies
-----------------------

You can create custom policies to supplement the system-defined policies of DMS for Kafka. For details about actions supported in custom policies, see "Permissions Policies and Supported Actions" in *Distributed Message Service API Reference*

To create a custom policy, choose either visual editor or JSON.

-  Visual editor: Select cloud services, actions, resources, and request conditions. This does not require knowledge of policy syntax.
-  JSON: Create a JSON policy or edit an existing one.

For details, see `Creating a Custom Policy <https://docs.otc.t-systems.com/en-us/usermanual/iam/iam_01_0016.html>`__. The following lists examples of common DMS for Kafka custom policies.

.. note::

   -  DMS for Kafka permissions policies are based on DMS. Therefore, when assigning permissions, select DMS permissions policies.
   -  Due to data caching, a policy involving Object Storage Service (OBS) actions will take effect five minutes after it is attached to a user, user group, or project.

-  Example 1: Grant permission to delete and restart instances.

   .. code-block::

      {
          "Version": "1.1",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "dms:instance:modifyStatus",
                      "dms:instance:delete"
                  ]
              }
          ]
      }

-  Example 2: Grant permission to deny instance deletion.

   A policy with only "Deny" permissions must be used together with other policies. If the permissions granted to an IAM user contain both "Allow" and "Deny", the "Deny" permissions take precedence over the "Allow" permissions.

   Assume that you want to grant the permissions of the **DMS FullAccess** policy to a user but want to prevent them from deleting instances. You can create a custom policy for denying instance deletion, and attach this policy together with the **DMS FullAccess** policy to the user. As an explicit deny in any policy overrides any allows, the user can perform all operations on DMS for Kafka excepting deleting instances.

   Example policy denying instance deletion:

   .. code-block::

      {
              "Version": "1.1",
              "Statement": [
                      {
                              "Effect": "Deny",
                              "Action": [
                                      "dms:instance:delete"
                              ]
                      }
              ]
      }

DMS for Kafka Resources
-----------------------

A resource is an object that exists within a service. DMS for Kafka resources include **kafka**. To select these resources, specify their paths.

.. table:: **Table 1** DMS for Kafka resources and their paths

   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | Resource              | Resource Name         | Path                                                                                                                                              |
   +=======================+=======================+===================================================================================================================================================+
   | kafka                 | Instance              | [Format]                                                                                                                                          |
   |                       |                       |                                                                                                                                                   |
   |                       |                       | DMS:``*``:``*``: kafka:*instance ID*                                                                                                              |
   |                       |                       |                                                                                                                                                   |
   |                       |                       | [Notes]                                                                                                                                           |
   |                       |                       |                                                                                                                                                   |
   |                       |                       | For instance resources, IAM automatically generates the prefix (**DMS:*:*:kafka:**) of the resource path.                                         |
   |                       |                       |                                                                                                                                                   |
   |                       |                       | For the path of a specific resource, add the *instance ID* to the end. You can also use an asterisk **\*** to indicate any resource. For example: |
   |                       |                       |                                                                                                                                                   |
   |                       |                       | **DMS:*:*:kafka:\*** indicates any Kafka instance.                                                                                                |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+

DMS for Kafka Request Conditions
--------------------------------

Request conditions are useful in determining when a custom policy is in effect. A request condition consists of condition keys and operators. Condition keys are either global or service-level and are used in the Condition element of a policy statement. `Global condition keys <https://docs.otc.t-systems.com/en-us/usermanual/iam/iam_01_0017.html>`__ (starting with **g:**) are available for operations of all services, while service-specific condition keys (starting with a service name such as **dms:**) are available only for operations of specific services. An operator must be used together with a condition key to form a complete condition statement.

DMS for Kafka has a group of predefined condition keys that can be used in IAM. For example, to define an "Allow" permission, use the condition dms:ssl to filter instances by SASL configurations. The following table lists the DMS for Kafka predefined condition keys.

.. table:: **Table 2** Predefined condition keys of DMS for Kafka

   ============= ======== ================================
   Condition Key Operator Description
   ============= ======== ================================
   dms:publicIP  Bool     Whether public access is enabled
   dms:ssl       Bool     Whether SSL is enabled
   ============= ======== ================================
