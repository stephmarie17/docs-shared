The {+driver-short+} provides helper methods for the following operators:

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Operator
     - Description

   * - :atlas:`autocomplete </atlas-search/autocomplete/>`
     - Performs a search for a word or phrase that contains a sequence of
       characters from an incomplete input string.  

   * - :atlas:`compound </atlas-search/compound/>`
     - Combines two or more operators into a single query. 

   * - :atlas:`equals </atlas-search/equals/>` 
     - Checks whether a field matches a value you specify.
       Maps to the ``equals()`` and ``equalsNull()`` methods

   * - :atlas:`exists </atlas-search/exists/>`
     - Tests if a path to a specified indexed field name exists in a document. 

   * - :atlas:`in </atlas-search/in/>`
     - Performs a search for an array of BSON number, date, boolean, objectId,
       uuid, or string values at the given path and returns documents where the
       value of the field equals any value in the specified array.  

   * - :atlas:`moreLikeThis </atlas-search/moreLikeThis/>`
     - Returns documents similar to input documents.  

   * - :atlas:`near </atlas-search/near/>`
     - Supports querying and scoring numeric, date, and GeoJSON point values. 

   * - :atlas:`phrase </atlas-search/phrase/>`
     - Performs a search for documents containing an ordered sequence of terms
       using the analyzer specified in the index configuration.  

   * - :atlas:`queryString  </atlas-search/queryString/>`
     - Supports querying a combination of indexed fields and values.  

   * - :atlas:`range </atlas-search/range/>` 
     - Supports querying and scoring numeric, date, and string values. 
       Maps to the ``numberRange()`` and ``dateRange()`` methods

   * - :atlas:`regex </atlas-search/regex/>`
     - Interprets the query field as a regular expression.   

   * - :atlas:`text </atlas-search/text/>`
     - Performs a full-text search using the analyzer that you specify in the
       index configuration.  

   * - :atlas:`wildcard </atlas-search/wildcard/>`
     - Enables queries which use special characters in the search string that
       can match any character.  

Example Pipeline Search Stage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note:: Atlas Sample Dataset

   This example uses the ``sample_mflix.movies`` collection from the Atlas sample
   datasets. To learn how to set up a free-tier Atlas cluster and load the
   sample dataset, see the :atlas:`Get Started with Atlas </getting-started/>` tutorial
   in the Atlas documentation.

Before you can run this example, you must create an Atlas Search index on the ``movies``
collection that has the following definition:

.. code-block:: json

   {
     "mappings": {
       "dynamic": true,
       "fields": {
         "title": {
           "analyzer": "lucene.keyword",
           "type": "string"
         }
       }
     }
   }

To learn more about creating Atlas Search indexes, see |as-idx-link|.

The following code creates a ``$search`` stage that has the following
specifications:

- Searches the ``genres`` array for the term ``"drama"``
- Searches the ``cast`` array for the phrase ``"sylvester stallone"``, accounting for possible misspellings
- Matches ``year`` values between ``1980`` and ``1989``, inclusive
- Searches for ``title`` values that begins with the term ``"Rocky"``

|atlas-query-operators-example|

To learn more about the Atlas Search helper methods, see the
`SearchOperator <{+core-api+}/client/model/search/SearchOperator.html>`__ interface reference
in the Driver Core API documentation.
