SearchOperator Helper Methods
-----------------------------

The {+driver-short+} provides helper methods for the following operations:

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - Operation
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

   This example uses the MongoDB Atlas sample dataset. Specifically, the
   ``movies`` collection in the ``sample_mflix`` database. You can learn how
   to  set up your own free-tier Atlas cluster and how to load the sample dataset
   in our :ref:`quick start guide <java-get-started>`.

The following code creates a search stage for a pipeline with the following filters:

- Movies in the drama genre
- Movies that include Sylvester Stallone in the cast, accounting for possible misspellings
- Movies made between 1980 and 1989, inclusive
- Movies with titles that begin with the word ``"Rocky"``

|atlas-query-operators-example|

To learn more about the helper methods, see the |searchoperator-interface-api-docs|.