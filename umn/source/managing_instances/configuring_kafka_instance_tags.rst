:original_name: TagManagement.html

.. _TagManagement:

Configuring Kafka Instance Tags
===============================

Tags facilitate Kafka instance identification and management.

You can add tags to a Kafka instance when creating the instance or add tags on the **Tags** page of the created instance. Tags can be deleted.

A tag consists of a tag key and a tag value. :ref:`Table 1 <tagmanagement__table193611920984>` lists the tag key and value requirements.

.. _tagmanagement__table193611920984:

.. table:: **Table 1** Tag key and value requirements

   +-----------------------------------+-------------------------------------------------------------------------+
   | Parameter                         | Requirements                                                            |
   +===================================+=========================================================================+
   | Tag key                           | -  Cannot be left blank.                                                |
   |                                   | -  Must be unique for the same instance.                                |
   |                                   | -  Can contain 1 to 128 characters.                                     |
   |                                   | -  Can contain letters, digits, spaces, and special characters \_.:=+-@ |
   |                                   | -  Cannot start or end with a space.                                    |
   |                                   | -  Cannot start with **\_sys\_**.                                       |
   +-----------------------------------+-------------------------------------------------------------------------+
   | Tag value                         | -  Can contain 0 to 255 characters.                                     |
   |                                   | -  Can contain letters, digits, spaces, and special characters \_.:=+-@ |
   |                                   | -  Cannot start or end with a space in instance creation.               |
   +-----------------------------------+-------------------------------------------------------------------------+

Notes and Constraints
---------------------

Up to 20 tags can be added to a Kafka instance.

Procedure
---------

#. Log in to the console.
#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired instance to go to the instance details page.
#. In the navigation pane, choose **Tags**.
#. Add or delete tags as required.

   -  Add a tag

      a. Click **Create/Delete Tag**.

      b. Enter a tag key and a tag value, and click **Add**.

         If you have predefined tags, select a predefined pair of tag key and value, and click **Add**.

      c. Click **OK**.

         View the new tag on the tag list page.

   -  Delete a tag

      Delete a tag using either of the following methods:

      -  In the row containing the tag to be deleted, click **Delete**. In the **Delete Tag** dialog box, click **Yes**.

      -  Click **Create/Delete Tag**. In the dialog box that is displayed, click |image1| next to the tag to be deleted and click **OK**.

         You can delete up to **19** tags in this way.

      -  Select one or more tags and click **Delete** above. The **Delete Tag** dialog box is displayed. Click **OK**.

      The tags are deleted when they are no longer displayed in the tag list.

.. |image1| image:: /_static/images/en-us_image_0000002157871349.png
