Overview
--------

JSON is a data format that represents the values of objects, arrays, numbers,
strings, booleans, and nulls. The **Extended JSON** format defines a reserved
set of keys prefixed with "``$``" to represent field type information that
directly corresponds to each type in BSON, the format that MongoDB uses to
store data.

To learn more about JSON, BSON, and Extended JSON, see
`our article about JSON and BSON <https://www.mongodb.com/resources/basics/json-and-bson>`__
and :manual:`Extended JSON </reference/mongodb-extended-json/>` in the {+mdb-server+} manual.

Extended JSON Formats
---------------------

MongoDB Extended JSON features different string formats to represent BSON data.
Each of the different formats conform to the JSON RFC
and meet specific use cases. The **extended** format, also known as the
**canonical** format, features specific representations for every BSON type
for bidirectional conversion without loss of information. The **Relaxed mode**
format is more concise and closer to ordinary JSON, but does not represent
all the type information such as the specific byte size of number fields.

See the following table to see a description of each format:

.. list-table::
   :header-rows: 1
   :stub-columns: 1
   :widths: 10 40

   * - Name
     - Description

   * - **Extended**
     - | Also known as the *canonical* format, this JSON representation avoids loss of
         BSON type information.
       | This format prioritizes type preservation at the loss of human-readability and
         interoperability with older formats. |driver-specific-text-extended|

   * - **Relaxed**
     - | JSON representation that describes BSON documents with some type information loss.
       | This format prioritizes human-readability and interoperability at the loss of
         certain type information. |driver-specific-text-relaxed|

   * - **Shell**
     - | JSON representation that matches the syntax used in the MongoDB shell.
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
