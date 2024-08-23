:original_name: api-grant-policy.html

.. _api-grant-policy:

Permissions and Supported Actions
=================================

This chapter describes fine-grained permissions management for your Kafka instances. If your account does not need individual IAM users, then you may skip over this chapter.

By default, new IAM users do not have permissions assigned. You need to add a user to one or more groups, and attach permissions policies or roles to these groups. Users inherit permissions from the groups to which they are added and can perform specified operations on cloud services based on the permissions.

You can grant users permissions by using roles and policies. Roles are a type of coarse-grained authorization mechanism that defines permissions related to user responsibilities. Policies define API-based permissions for operations on specific resources under certain conditions, allowing for more fine-grained, secure access control of cloud resources.

For details about DMS system policies, see `Permissions Management <https://docs.otc.t-systems.com/en-us/usermanual/dms/UserPrivilegeManagement.html>`__.

.. note::

   Policy-based authorization is useful if you want to allow or deny the access to an API.

An account has all of the permissions required to call all APIs, but IAM users must be assigned the required permissions. The permissions required for calling an API are determined by the actions supported by the API. Only users who have been granted permissions allowing the actions can call the API successfully. For example, if an IAM user wants to query Kafka instances using an API, the user must have been granted permissions that allow the **dms:instance:create** action.

Supported Actions
-----------------

DMS for Kafka provides system-defined policies that can be directly used in IAM. You can also create custom policies and use them to supplement system-defined policies, implementing more refined access control. Operations supported by policies are specific to APIs. The following are common concepts related to policies:

-  Permission: a statement in a policy that allows or denies certain operations.
-  APIs: REST APIs that can be called by a user who has been granted specific permissions.
-  Action: Specific operations that are allowed or denied.
-  IAM projects or enterprise projects: A custom policy can be applied to IAM projects or enterprise projects or both. Policies that contain actions for both IAM and enterprise projects can be used and take effect for both IAM and Enterprise Management. Policies that only contain actions for IAM projects can be used and only take effect for IAM. Administrators can check whether an action supports IAM projects or enterprise projects in the action list.

DMS supports the following actions in custom policies:

-  :ref:`Lifecycle management actions <api-grant-policy__section19410185916427>`, including actions supported by Kafka instance lifecycle management APIs, such as the APIs for creating an instance, querying the instance list, modifying instance information, and batch restarting or deleting instances.
-  :ref:`Instance management actions <api-grant-policy__section8384018382>`, including actions supported by Kafka instance management APIs, such as the APIs for resetting passwords and configuring automatic topic creation.
-  :ref:`Smart Connect actions <api-grant-policy__section17532240105412>`, including actions supported by Smart Connect APIs, such as the APIs for enabling or disabling Smart Connect, creating a Smart Connect task.
-  :ref:`Specification modification management action <api-grant-policy__section87441363582>`, supported by the specification modification management API for modifying instance specifications.
-  :ref:`Topic management actions <api-grant-policy__section11586915535>`, including actions supported by topic management APIs, such as the APIs for creating, querying, and modifying topics.
-  :ref:`User management actions <api-grant-policy__section56931740695>`, including actions supported by user management APIs, such as the APIs for creating users, querying users, and configuring user permissions.
-  :ref:`Message query actions <api-grant-policy__section9674351127>`, including actions supported by message query APIs, such as the API for querying messages.
-  :ref:`Background task management actions <api-grant-policy__section17202057191519>`, including actions supported by background task management APIs, such as the APIs for querying the background task list of an instance and querying a specified background task.
-  :ref:`Tag management actions <api-grant-policy__section1648562652120>`, including actions supported by tag management APIs, such as the APIs for querying instance tags and project tags.

.. _api-grant-policy__section19410185916427:

Lifecycle Management
--------------------

.. table:: **Table 1** Lifecycle management

   +----------------------------------------+-------------------------------------------------+------------------------------------+-------------+----------------------+
   | Permission                             | API                                             | Action                             | IAM         | Enterprise           |
   |                                        |                                                 |                                    |             |                      |
   |                                        |                                                 |                                    | (Project)   | (Enterprise Project) |
   +========================================+=================================================+====================================+=============+======================+
   | Creating an instance                   | POST /v2/{engine}/{project_id}/instances        | dms:instance:create                | Y           | Y                    |
   +----------------------------------------+-------------------------------------------------+------------------------------------+-------------+----------------------+
   | Querying all instances                 | GET /v2/{project_id}/instances                  | dms:instance:list                  | Y           | Y                    |
   +----------------------------------------+-------------------------------------------------+------------------------------------+-------------+----------------------+
   | Querying an instance                   | GET /v2/{project_id}/instances/{instance_id}    | dms:instance:get                   | Y           | Y                    |
   +----------------------------------------+-------------------------------------------------+------------------------------------+-------------+----------------------+
   | Deleting an instance                   | DELETE /v2/{project_id}/instances/{instance_id} | dms:instance:delete                | Y           | Y                    |
   +----------------------------------------+-------------------------------------------------+------------------------------------+-------------+----------------------+
   | Modifying instance information         | PUT /v2/{project_id}/instances/{instance_id}    | dms:instance:modify                | Y           | Y                    |
   +----------------------------------------+-------------------------------------------------+------------------------------------+-------------+----------------------+
   | Batch restarting or deleting instances | POST /v2/{project_id}/instances/action          | Restart: dms:instance:modifyStatus | Y           | Y                    |
   |                                        |                                                 |                                    |             |                      |
   |                                        |                                                 | Delete: dms:instance:delete        |             |                      |
   +----------------------------------------+-------------------------------------------------+------------------------------------+-------------+----------------------+

.. _api-grant-policy__section8384018382:

Instance Management
-------------------

.. table:: **Table 2** Instance management

   +-----------------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------------+-------------+----------------------+
   | Permission                                                | API                                                                                          | Action                     | IAM         | Enterprise           |
   |                                                           |                                                                                              |                            |             |                      |
   |                                                           |                                                                                              |                            | (Project)   | (Enterprise Project) |
   +===========================================================+==============================================================================================+============================+=============+======================+
   | Resetting a password                                      | POST /v2/{project_id}/instances/{instance_id}/password                                       | dms:instance:resetAuthInfo | Y           | Y                    |
   +-----------------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------------+-------------+----------------------+
   | Configuring automatic topic creation                      | POST /v2/{project_id}/instances/{instance_id}/autotopic                                      | dms:instance:modify        | Y           | Y                    |
   +-----------------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------------+-------------+----------------------+
   | Modifying the private IP address for cross-VPC access     | POST /v2/{project_id}/instances/{instance_id}/crossvpc/modify                                | dms:instance:modify        | Y           | Y                    |
   +-----------------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------------+-------------+----------------------+
   | Resetting consumer group offset to the specified position | POST /v2/{project_id}/instances/{instance_id}/management/groups/{group}/reset-message-offset | dms:instance:modify        | Y           | Y                    |
   +-----------------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------------+-------------+----------------------+

.. _api-grant-policy__section17532240105412:

Smart Connect
-------------

.. table:: **Table 3** Smart Connect

   +------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+--------------------------------------+--------------+---------------------+
   | Permission                                                                         | API                                                                                  | Action                               | IAM Projects | Enterprise Projects |
   +====================================================================================+======================================================================================+======================================+==============+=====================+
   | Enabling Smart Connect                                                             | POST /v2/{project_id}/instances/{instance_id}/connector                              | dms:instance:connector               | Y            | Y                   |
   +------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+--------------------------------------+--------------+---------------------+
   | Disabling Smart Connect                                                            | POST /v2/{project_id}/kafka/instances/{instance_id}/delete-connector                 | dms:instance:connector               | Y            | Y                   |
   +------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+--------------------------------------+--------------+---------------------+
   | Creating a Smart Connect task                                                      | POST /v2/{project_id}/instances/{instance_id}/connector/tasks                        | dms:instance:createConnectorSinkTask | Y            | Y                   |
   +------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+--------------------------------------+--------------+---------------------+
   | Listing Smart Connect tasks                                                        | GET /v2/{project_id}/instances/{instance_id}/connector/tasks                         | dms:instance:listConnectorSinkTask   | Y            | Y                   |
   +------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+--------------------------------------+--------------+---------------------+
   | Querying Smart Connect task details                                                | GET /v2/{project_id}/instances/{instance_id}/connector/tasks/{task_id}               | dms:instance:getConnectorSinkTask    | Y            | Y                   |
   +------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+--------------------------------------+--------------+---------------------+
   | Deleting Smart Connect tasks                                                       | DELETE /v2/{project_id}/instances/{instance_id}/connector/tasks/{task_id}            | dms:instance:deleteConnectorSinkTask | Y            | Y                   |
   +------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+--------------------------------------+--------------+---------------------+
   | Pausing Smart Connect tasks                                                        | PUT /v2/{project_id}/instances/{instance_id}/connector/tasks/{task_id}/pause         | dms:instance:updateConnectorTask     | Y            | Y                   |
   +------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+--------------------------------------+--------------+---------------------+
   | Restarting Smart Connect tasks                                                     | PUT /v2/{project_id}/instances/{instance_id}/connector/tasks/{task_id}/resume        | dms:instance:updateConnectorTask     | Y            | Y                   |
   +------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+--------------------------------------+--------------+---------------------+
   | Starting a Smart Connect task or restarting a paused or running Smart Connect task | PUT /v2/{project_id}/kafka/instances/{instance_id}/connector/tasks/{task_id}/restart | dms:instance:updateConnectorTask     | Y            | Y                   |
   +------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+--------------------------------------+--------------+---------------------+

.. _api-grant-policy__section87441363582:

Specification Modification Management
-------------------------------------

.. table:: **Table 4** Specification modification management

   +-----------------------------------+---------------------------------------------------------------+--------------------+--------------+---------------------+
   | Permission                        | API                                                           | Action             | IAM Projects | Enterprise Projects |
   +===================================+===============================================================+====================+==============+=====================+
   | Modifying instance specifications | POST /v2/{engine}/{project_id}/instances/{instance_id}/extend | dms:instance:scale | Y            | Y                   |
   +-----------------------------------+---------------------------------------------------------------+--------------------+--------------+---------------------+

.. _api-grant-policy__section11586915535:

Topic Management
----------------

.. table:: **Table 5** Topic management

   +------------------------------------------------+-------------------------------------------------------------+---------------------+--------------+---------------------+
   | Permission                                     | API                                                         | Action              | IAM Projects | Enterprise Projects |
   +================================================+=============================================================+=====================+==============+=====================+
   | Creating a topic in a Kafka instance           | POST /v2/{project_id}/instances/{instance_id}/topics        | dms:instance:modify | Y            | Y                   |
   +------------------------------------------------+-------------------------------------------------------------+---------------------+--------------+---------------------+
   | Querying a topic in a Kafka instance           | GET /v2/{project_id}/instances/{instance_id}/topics         | dms:instance:get    | Y            | Y                   |
   +------------------------------------------------+-------------------------------------------------------------+---------------------+--------------+---------------------+
   | Modifying topics of a Kafka instance           | PUT /v2/{project_id}/instances/{instance_id}/topics         | dms:instance:modify | Y            | Y                   |
   +------------------------------------------------+-------------------------------------------------------------+---------------------+--------------+---------------------+
   | Deleting topics in a Kafka instance in batches | POST /v2/{project_id}/instances/{instance_id}/topics/delete | dms:instance:modify | Y            | Y                   |
   +------------------------------------------------+-------------------------------------------------------------+---------------------+--------------+---------------------+

.. _api-grant-policy__section56931740695:

User Management
---------------

.. table:: **Table 6** User management

   +---------------------------+-------------------------------------------------------------------------------+---------------------+--------------+---------------------+
   | Permission                | API                                                                           | Action              | IAM Projects | Enterprise Projects |
   +===========================+===============================================================================+=====================+==============+=====================+
   | Querying the user list    | GET /v2/{project_id}/instances/{instance_id}/users                            | dms:instance:get    | Y            | Y                   |
   +---------------------------+-------------------------------------------------------------------------------+---------------------+--------------+---------------------+
   | Creating a user           | POST /v2/{project_id}/instances/{instance_id}/users                           | dms:instance:modify | Y            | Y                   |
   +---------------------------+-------------------------------------------------------------------------------+---------------------+--------------+---------------------+
   | Deleting users in batches | PUT /v2/{project_id}/instances/{instance_id}/users                            | dms:instance:modify | Y            | Y                   |
   +---------------------------+-------------------------------------------------------------------------------+---------------------+--------------+---------------------+
   | Resetting a user password | PUT /v2/{project_id}/instances/{instance_id}/users/{user_name}                | dms:instance:get    | Y            | Y                   |
   +---------------------------+-------------------------------------------------------------------------------+---------------------+--------------+---------------------+
   | Querying user permissions | GET /v1/{project_id}/instances/{instance_id}/topics/{topic_name}/accesspolicy | dms:instance:get    | Y            | Y                   |
   +---------------------------+-------------------------------------------------------------------------------+---------------------+--------------+---------------------+
   | Granting user permissions | POST /v1/{project_id}/instances/{instance_id}/topics/accesspolicy             | dms:instance:modify | Y            | Y                   |
   +---------------------------+-------------------------------------------------------------------------------+---------------------+--------------+---------------------+

.. _api-grant-policy__section9674351127:

Message Query
-------------

.. table:: **Table 7** Message query

   +-------------------+-------------------------------------------------------+------------------+--------------+---------------------+
   | Permission        | API                                                   | Action           | IAM Projects | Enterprise Projects |
   +===================+=======================================================+==================+==============+=====================+
   | Querying messages | GET /v2/{project_id}/instances/{instance_id}/messages | dms:instance:get | Y            | Y                   |
   +-------------------+-------------------------------------------------------+------------------+--------------+---------------------+

.. _api-grant-policy__section17202057191519:

Background Task Management
--------------------------

.. table:: **Table 8** Background task management

   +----------------------------+-----------------------------------------------------------------+-----------------------------------+--------------+---------------------+
   | Permission                 | API                                                             | Action                            | IAM Projects | Enterprise Projects |
   +============================+=================================================================+===================================+==============+=====================+
   | Listing background tasks   | GET /v2/{project_id}/instances/{instance_id}/tasks              | dms:instance:getBackgroundTask    | Y            | Y                   |
   +----------------------------+-----------------------------------------------------------------+-----------------------------------+--------------+---------------------+
   | Querying a background task | GET /v2/{project_id}/instances/{instance_id}/tasks/{task_id}    | dms:instance:getBackgroundTask    | Y            | Y                   |
   +----------------------------+-----------------------------------------------------------------+-----------------------------------+--------------+---------------------+
   | Deleting a background task | DELETE /v2/{project_id}/instances/{instance_id}/tasks/{task_id} | dms:instance:deleteBackgroundTask | Y            | Y                   |
   +----------------------------+-----------------------------------------------------------------+-----------------------------------+--------------+---------------------+

.. _api-grant-policy__section1648562652120:

Tag Management
--------------

.. table:: **Table 9** Tag management

   +-------------------------------+-------------------------------------------------------+---------------------+--------------+---------------------+
   | Permission                    | API                                                   | Action              | IAM Projects | Enterprise Projects |
   +===============================+=======================================================+=====================+==============+=====================+
   | Batch adding or deleting tags | POST /v2/{project_id}/kafka/{instance_id}/tags/action | dms:instance:modify | Y            | Y                   |
   +-------------------------------+-------------------------------------------------------+---------------------+--------------+---------------------+
   | Listing tags of an instance   | GET /v2/{project_id}/kafka/{instance_id}/tags         | dms:instance:get    | Y            | Y                   |
   +-------------------------------+-------------------------------------------------------+---------------------+--------------+---------------------+
   | Listing tags of a project     | GET /v2/{project_id}/kafka/tags                       | dms:instance:get    | Y            | Y                   |
   +-------------------------------+-------------------------------------------------------+---------------------+--------------+---------------------+
