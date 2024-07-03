:original_name: ProductDescPrivilegeManagement.html

.. _ProductDescPrivilegeManagement:

Permission
==========

You can use Identity and Access Management (IAM) to manage DMS for Kafka permissions and control access to your resources. IAM provides identity authentication, permissions management, and access control.

You can create IAM users for your employees, and assign permissions to these users on a principle of least privilege (PoLP) basis to control their access to specific resource types. For example, you can create IAM users for software developers and assign specific permissions to allow them to use Kafka instance resources but prevent them from being able to delete resources or perform any high-risk operations.

If your account does not require individual IAM users for permissions management, skip this section.

IAM is a free service. You only pay for the resources in your account.

For more information, see `IAM Service Overview <https://docs.otc.t-systems.com/en-us/usermanual/iam/iam_01_0026.html>`__.

DMS Permissions
---------------

By default, new IAM users do not have any permissions assigned. To assign permissions to these new users, add them to one or more groups, and attach permissions policies or roles to these groups.

DMS is a project-level service deployed and accessed in specific physical regions. When assigning DMS for Kafka permissions to a user group, specify region-specific projects where the permissions will take effect. If you select **All projects**, the permissions will be granted for all region-specific projects. When accessing DMS, the users need to switch to a region where they have been authorized to use this service.

You can grant permissions by using roles and policies.

-  Roles: A type of coarse-grained authorization mechanism that provides only a limited number of service-level roles. When using roles to grant permissions, you also need to assign dependency roles. However, roles are not an ideal choice for fine-grained authorization and secure access control.
-  Policies: A fine-grained authorization strategy that defines permissions required to perform operations on specific cloud resources under certain conditions. This mechanism allows for more flexible policy-based authorization for more secure access control. For example, you can grant DMS for Kafka users only the permissions for managing instances. Most policies define permissions based on APIs. For the API actions supported by DMS for Kafka, see "Permissions Policies and Supported Actions" in the *Distributed Message Service API Reference*.

:ref:`Table 1 <productdescprivilegemanagement__en-us_topic_0170871404_table8486434381>` lists all the system-defined policies supported by DMS for Kafka.

.. _productdescprivilegemanagement__en-us_topic_0170871404_table8486434381:

.. table:: **Table 1** System-defined policies supported by DMS for Kafka

   +--------------------+---------------------------------------------------------------------------------------------------------------------+-----------------------+------------+
   | Role/Policy Name   | Description                                                                                                         | Type                  | Dependency |
   +====================+=====================================================================================================================+=======================+============+
   | DMS FullAccess     | Administrator permissions for DMS. Users granted these permissions can perform all operations on DMS.               | System-defined policy | None       |
   +--------------------+---------------------------------------------------------------------------------------------------------------------+-----------------------+------------+
   | DMS UserAccess     | Common user permissions for DMS, excluding permissions for creating, modifying, deleting, and scaling up instances. | System-defined policy | None       |
   +--------------------+---------------------------------------------------------------------------------------------------------------------+-----------------------+------------+
   | DMS ReadOnlyAccess | Read-only permissions for DMS. Users granted these permissions can only view DMS data.                              | System-defined policy | None       |
   +--------------------+---------------------------------------------------------------------------------------------------------------------+-----------------------+------------+
   | DMS VPCAccess      | VPC operation permissions to assign to DMS agencies.                                                                | System-defined policy | None       |
   +--------------------+---------------------------------------------------------------------------------------------------------------------+-----------------------+------------+
   | DMS KMSAccess      | KMS operation permissions to assign to DMS agencies.                                                                | System-defined policy | None       |
   +--------------------+---------------------------------------------------------------------------------------------------------------------+-----------------------+------------+

.. note::

   System-defined policies contain OBS actions. Due to data caching, the policies take effect five minutes after they are attached to a user, user group, or enterprise project.

:ref:`Table 2 <productdescprivilegemanagement__en-us_topic_0170871404_table12985122891519>` lists the common operations supported by each DMS for Kafka system policy. Select the policies as required.

.. _productdescprivilegemanagement__en-us_topic_0170871404_table12985122891519:

.. table:: **Table 2** Common operations supported by each system-defined policy of DMS for Kafka

   +-----------------------------------+----------------+----------------+--------------------+---------------+---------------+
   | Operation                         | DMS FullAccess | DMS UserAccess | DMS ReadOnlyAccess | DMS VPCAccess | DMS KMSAccess |
   +===================================+================+================+====================+===============+===============+
   | Creating instances                | Y              | x              | x                  | x             | x             |
   +-----------------------------------+----------------+----------------+--------------------+---------------+---------------+
   | Modifying instances               | Y              | x              | x                  | x             | x             |
   +-----------------------------------+----------------+----------------+--------------------+---------------+---------------+
   | Deleting instances                | Y              | x              | x                  | x             | x             |
   +-----------------------------------+----------------+----------------+--------------------+---------------+---------------+
   | Modifying instance specifications | Y              | x              | x                  | x             | x             |
   +-----------------------------------+----------------+----------------+--------------------+---------------+---------------+
   | Restarting instances              | Y              | Y              | x                  | x             | x             |
   +-----------------------------------+----------------+----------------+--------------------+---------------+---------------+
   | Querying instance information     | Y              | Y              | Y                  | x             | x             |
   +-----------------------------------+----------------+----------------+--------------------+---------------+---------------+

Fine-grained Authorization
--------------------------

To use a custom fine-grained policy, log in to the IAM console as an administrator and select the desired fine-grained permissions for DMS. :ref:`Table 3 <productdescprivilegemanagement__table0874182025919>` describes fine-grained permission dependencies of DMS for Kafka.

.. _productdescprivilegemanagement__table0874182025919:

.. table:: **Table 3** Fine-grained permission dependencies of DMS for Kafka

   +-----------------------------------+---------------------------------+---------------------------+
   | Permission                        | Description                     | Dependency                |
   +===================================+=================================+===========================+
   | dms:instance:list                 | Viewing the instance list       | None                      |
   +-----------------------------------+---------------------------------+---------------------------+
   | dms:instance:get                  | Viewing instance details        | None                      |
   +-----------------------------------+---------------------------------+---------------------------+
   | dms:instance:create               | Creating an instance            | -  vpc:vpcs:get           |
   |                                   |                                 | -  vpc:ports:create       |
   |                                   |                                 | -  vpc:securityGroups:get |
   |                                   |                                 | -  vpc:ports:get          |
   |                                   |                                 | -  vpc:subnets:get        |
   |                                   |                                 | -  vpc:vpcs:list          |
   |                                   |                                 | -  vpc:publicIps:get      |
   |                                   |                                 | -  vpc:publicIps:list     |
   |                                   |                                 | -  vpc:ports:update       |
   |                                   |                                 | -  vpc:publicIps:update   |
   |                                   |                                 | -  vpc:ports:delete       |
   |                                   |                                 | -  kms:cmk:list           |
   +-----------------------------------+---------------------------------+---------------------------+
   | dms:instance:getBackgroundTask    | Viewing background task details | None                      |
   +-----------------------------------+---------------------------------+---------------------------+
   | dms:instance:deleteBackgroundTask | Deleting a background task      | None                      |
   +-----------------------------------+---------------------------------+---------------------------+
   | dms:instance:modifyStatus         | Restarting an instance          | None                      |
   +-----------------------------------+---------------------------------+---------------------------+
   | dms:instance:resetAuthInfo        | Resetting an instance password  | None                      |
   +-----------------------------------+---------------------------------+---------------------------+
   | dms:instance:modifyAuthInfo       | Changing an instance password   | None                      |
   +-----------------------------------+---------------------------------+---------------------------+
   | dms:instance:modify               | Modifying an instance           | -  vpc:vpcs:get           |
   |                                   |                                 | -  vpc:ports:create       |
   |                                   |                                 | -  vpc:securityGroups:get |
   |                                   |                                 | -  vpc:ports:get          |
   |                                   |                                 | -  vpc:subnets:get        |
   |                                   |                                 | -  vpc:vpcs:list          |
   |                                   |                                 | -  vpc:publicIps:get      |
   |                                   |                                 | -  vpc:publicIps:list     |
   |                                   |                                 | -  vpc:ports:update       |
   |                                   |                                 | -  vpc:publicIps:update   |
   |                                   |                                 | -  vpc:ports:delete       |
   +-----------------------------------+---------------------------------+---------------------------+
   | dms:instance:scale                | Scaling up an instance          | -  vpc:vpcs:get           |
   |                                   |                                 | -  vpc:ports:create       |
   |                                   |                                 | -  vpc:securityGroups:get |
   |                                   |                                 | -  vpc:ports:get          |
   |                                   |                                 | -  vpc:subnets:get        |
   |                                   |                                 | -  vpc:vpcs:list          |
   |                                   |                                 | -  vpc:publicIps:get      |
   |                                   |                                 | -  vpc:publicIps:list     |
   |                                   |                                 | -  vpc:ports:update       |
   |                                   |                                 | -  vpc:publicIps:update   |
   +-----------------------------------+---------------------------------+---------------------------+
   | dms:instance:delete               | Deleting an instance            | None                      |
   +-----------------------------------+---------------------------------+---------------------------+
