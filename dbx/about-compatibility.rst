==========================
About Driver Compatibility
==========================

Each MongoDB Driver includes two compatibility tables: one for MongoDB and one for the language the driver supports. Before performing an upgrade, use these tables to ensure your environment will remain operational. 

Read the following section for detailed explanations of each table.

.. _mongodb-compatibility-table-about-{+driver+}:

MongoDB Compatibility Table
---------------------------

In the **MongoDB Compatibility** table, each column represents a version of 
version of MongoDB server and each row represents a major release
version of the driver.

* A check mark (✓) means that the driver can use all features of that version of MongoDB server.
* A circled asterisk (⊛) means that the driver works with that version of MongoDB server, but it can't use every new feature.
* An empty cell means that the driver hasn't been tested with that version of MongoDB server.

.. important:: 
    
    Avoid using any driver version that isn't in the compatibility table.

If you're **upgrading your server version**, your current driver will still work, but  you may not be able to use new MongoDB features. We recommend using the newest
compatible driver when upgrading your server version.

If you're **upgrading your driver version**, choose the newest version that's compatible with your version of MongoDB server. 

.. note::

    Minor and patch versions have the same compatibility as their major version.

.. _language-compatibility-table-about-{+driver+}:

Language Compatibility Table
----------------------------

In the **Language Compatibility** table, each column represents a version of the driver language (e.g., Node.js or Python) and each row represents a major release
version of the driver.

* A check mark (✓) means that the driver is fully compatible with that version of the language.
* An empty cell means that the driver hasn't been tested with that version of the language.
