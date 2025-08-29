Overview
--------

In this guide, you can learn how to use the **Extended JSON** data format
when interacting with MongoDB documents.

JSON is a human-readable data format that represents the values of objects,
arrays, numbers, strings, booleans, and nulls. This format supports only a
subset of BSON data types, which is the format that MongoDB uses to store data. The
Extended JSON format supports more BSON types, defining a reserved
set of keys prefixed with "``$``" to represent field type information that
directly corresponds to each type in BSON.

To learn more about JSON, BSON, and Extended JSON, see the
`JSON and BSON <https://www.mongodb.com/resources/basics/json-and-bson>`__ resource
and :manual:`Extended JSON </reference/mongodb-extended-json/>` {+mdb-server+} manual
entry.

Extended JSON Formats
---------------------

MongoDB Extended JSON provides string formats to represent BSON data.
Each format conforms to the `JSON RFC <https://www.rfc-editor.org/rfc/rfc8259>`__
and meets specific use cases.

The following table describes each Extended JSON format:

.. list-table::
   :header-rows: 1
   :stub-columns: 1
   :widths: 10 40

   * - Name
     - Description

   * - **Extended** or **Canonical**
     - | A string format that avoids loss of BSON type information during data conversions.
       | This format prioritizes type preservation at the loss of human-readability and
         interoperability with older formats. |driver-specific-text-extended|

   * - **Relaxed**
     - | A string format that describes BSON documents with some type information loss.
       | This format prioritizes human-readability and interoperability at the loss of
         certain type information. |driver-specific-text-relaxed|

   * - **Shell**
     - | A string format that matches the syntax used in the MongoDB shell.
       | This format prioritizes compatibility with the MongoDB shell, which often uses
         JavaScript functions to represent types. |driver-specific-text-shell|

.. note::

   The {+driver-short+} parses the ``$uuid`` Extended JSON type from a string to a
   ``BsonBinary`` object of binary subtype 4. For more information about ``$uuid`` field
   parsing, see the
   :spec:`special rules for parsing $uuid fields </extended-json/extended-json.md#special-rules-for-parsing-uuid-fields>`
   section in the extended JSON specification.

.. _extended_json_example_section:

Extended JSON Examples
~~~~~~~~~~~~~~~~~~~~~~

The following examples show a document containing an ObjectId, date, and long
number field represented in each Extended JSON format. Click the tab that
corresponds to the format of the example you want to see:

.. tabs::

   .. tab:: Extended
      :tabid: extended-format

      .. code-block:: json

         {
           "_id": { "$oid": "573a1391f29313caabcd9637" },
           "createdAt": { "$date": { "$numberLong": "1601499609" }},
           "numViews": { "$numberLong": "36520312" }
         }

   .. tab:: Relaxed Mode
      :tabid: relaxed-mode-format

      .. code-block:: json

         {
           "_id": { "$oid": "573a1391f29313caabcd9637" },
           "createdAt": { "$date": "2020-09-30T18:22:51.648Z" },
           "numViews": 36520312
         }

   .. tab:: Shell
      :tabid: shell-format

      .. code-block:: json

         {
           "_id": ObjectId("573a1391f29313caabcd9637"),
           "createdAt": ISODate("2020-09-30T18:22:51.648Z"),
           "numViews": NumberLong("36520312")
         }
