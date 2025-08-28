Examples
~~~~~~~~

The scenarios below show several uses of the MongoDB Assistant. 

Connection Error
````````````````

If you get a connection error message, a pop-up will appear that directs you to
use the MongoDB Assistant to debug the error. Clicking "Debug for me" prompts the
assistant to automatically generate a prompt to diagnose the error.

Input:

.. code-block::

   Diagnose why my Compass connection is failing and help me debug it. 

   Connection string (password redacted): 
   mongodb+srv://user:****@cluster0.pndqllj.mongodb.net/

   Error message:
   querySrv ECONNREFUSED

Output:

.. code-block:: 

   This is possibly a DNS (network) or MongoDB Driver issue. Given that DNS srv
   queries sometimes behave differently than other DNS lookup types, we suggest
   the following next steps:

   1. Locate your "legacy" connection string in Atlas
      a. The lecacy connection string will start with mongodb:// instead of 
      mongodb+srv://
   2. Attempt to connect using the legacy connection string
   3. If the legacy connection string works, ensure you are using the latest 
      version of MongoDB Compass, share the findings of what works and what does
      not work with your network administrator
   4. If the legacy connection string does not work, follow troubleshooting steps
      for the next error (the error message is expected to change)

Explain Plan
````````````

Ask the MongoDB Assistant to analyze the output of your query:

Input: 

.. code-block::

   Interpret this explain plan output and tell me how to optimize my query:

   {"explainVersion":"1","stages":[{"$cursor":{"queryPlanner":{"namespace":"restaurants.nyc",
   "indexFilterSet":false,"parsedQuery":{"cuisine":{"$eq":"Italian"}},"queryHash":"0D9A721D",
   "planCacheKey":"0BC4F8A9","optimizationTimeMillis":0,"maxIndexedOrSolutionsReached":false,
   "maxIndexedAndSolutionsReached":false,"maxScansToExplodeReached":false,
   "winningPlan":{"stage":"PROJECTION_SIMPLE","transformBy":{"borough":1,"_id":0},
   "inputStage":{"stage":"FETCH","inputStage":{"stage":"IXSCAN","keyPattern":{"cuisine":-1},
   "indexName":"cuisine_-1","isMultiKey":false,"multiKeyPaths":{"cuisine":[]},
   "isUnique":false,"isSparse":false,"isPartial":false,"indexVersion":2,"direction":"forward",
   "indexBounds":{"cuisine":["[\"Italian\", \"Italian\"]"]}}}},"rejectedPlans":[]},
   "executionStats":{"executionSuccess":true,"nReturned":43207,"executionTimeMillis":1028,
   "totalKeysExamined":43207,"totalDocsExamined":43207,"executionStages":{"stage":"PROJECTION_SIMPLE",
   "nReturned":43207,"executionTimeMillisEstimate":888,"works":43208,
   "advanced":43207,"needTime":0,"needYield":0,"saveState":80,"restoreState":80,"isEOF":1,
   "transformBy":{"borough":1,"_id":0},"inputStage":{"stage":"FETCH","nReturned":43207,
   "executionTimeMillisEstimate":885,"works":43208,"advanced":43207,"needTime":0,
   "needYield":0,"saveState":80,"restoreState":80,"isEOF":1,"docsExamined":43207,
   "alreadyHasObj":0,"inputStage":{"stage":"IXSCAN","nReturned":43207,
   "executionTimeMillisEstimate":48,"works":43208,"advanced":43207,"needTime":0,
   "needYield":0,"saveState":80,"restoreState":80,"isEOF":1,"keyPattern":{"cuisine":-1},
   "indexName":"cuisine_-1","isMultiKey":false,"multiKeyPaths":{"cuisine":[]},
   "isUnique":false,"isSparse":false,"isPartial":false,"indexVersion":2,
   "direction":"forward","indexBounds":{"cuisine":["[\"Italian\", \"Italian\"]"]},
   "keysExamined":43207,"seeks":1,"dupsTested":0,"dupsDropped":0}}}}}}, "nReturned":43207,
   "executionTimeMillisEstimate":1004},{"$group":{"_id":"$borough",
   "count":{"$sum":{"$const":1}}},"maxAccumulatorMemoryUsageBytes":{"count":480},
   "totalOutputDataSizeBytes":1254,"usedDisk":false,"spills":0,"spilledDataStorageSize":0,
   "numBytesSpilledEstimate":0,"spilledRecords":0,"nReturned":5,
   "executionTimeMillisEstimate":1019}],
   "serverInfo":{"host":"atlas-mk8saw-shard-00-01.pndqllj.mongodb.net","port":27017,
   "version":"7.0.21","gitVersion":"a47b62aff2bae1914085c3ef1d90fc099acf000c"},
   "serverParameters":{"internalQueryFacetBufferSizeBytes":104857600,
   "internalQueryFacetMaxOutputDocSizeBytes":104857600,
   "internalLookupStageIntermediateDocumentMaxSizeBytes":104857600,
   "internalDocumentSourceGroupMaxMemoryBytes":104857600,
   "internalQueryMaxBlockingSortMemoryUsageBytes":104857600,
   "internalQueryProhibitBlockingMergeOnMongoS":0,"internalQueryMaxAddToSetBytes":104857600,
   "internalDocumentSourceSetWindowFieldsMaxMemoryBytes":104857600,
   "internalQueryFrameworkControl":"forceClassicEngine"},"command":{"aggregate":"nyc",
   "pipeline":[{"$match":{"cuisine":"Italian"}},{"$group":{"_id":"$borough",
   "count":{"$sum":1}}}],"cursor":{},"maxTimeMS":60000,"$db":"restaurants"},"ok":1,
   "$clusterTime":{"clusterTime":{"$timestamp":"7522966816189054977"},
   "signature":{"hash":"dhZ8X27p5jRJo1x/U9ZpF8L4eSc=","keyId":{"low":1,"high":1737746411,
   "unsigned":false}}},"operationTime":{"$timestamp":"7522966816189054977"}}

Output:

.. code-block:: 

   **Aggregation Pipeline Recap**

   This pipeline filters documents where cuisine is "Italian", then groups them
   by "borough", counting how many Italian restaurants exist in each borough. 

   **Execution Plan Breakdown**

   1. Stage 1- $match: { cuisine: "Italian" }
      - MongoDB uses the cuisine_ -1 index to identify matching documents (IXSCAN).
      - However, it performs a FETCH stage afterward, meaning it reads full 
        documents from disk- 43,207 in total.
      - Why? Because the index does not contain the borough field, which is needYield
        for grouping. 
   2. Stage 2- $group by borough
      - Performed in-memory, no disk spill (usedDisk: false).
      - Only 5 groups returned, minimal memory used (480 bytes).
   
   Performance Observations

   - Keys examined: 43,207
   - Documents examined: 43,207
   - Execution time: ~1s

   Optimization Suggestion 

   To eliminate the FETCH stage and significantly reduce I/O, you can create a 
   compound index that includes both cuisine and borough. If you choose to create
   the compound index, ensure that the index fields are selected in this order. 
   The order of fields in a compound index is very important. Here, cuisine is
   first used to filter the documents, so it must come before borough. 

   Along the same lines, if you create this compound index, you no longer need a 
   separate index on just the cuisine field. This is because MongoDB can use the
   prefixes of a compound index to optimize query execution. A query filtering 
   only on cuisine can efficiently use the prefix of the compound index, making a 
   standalone index on cuisine redundant. 

   Please note that creating an unnecessary index may be detrimental to your 
   application. New indexes require additional index storage and increase the 
   overhead for write operations. 

   Consider the pros and cons carefully when deciding whether or not to create a 
   new index. Also, think through when index makes the most sense for your application
   in the context of other queries frequently run. Please ask follow up questions
   if you'd like further guidance. 

User questions
``````````````

The following are examples of questions you can ask the MongoDB assistant about 
Compass/DE functions and queries. 

Input:

.. code-block::

   How is MongoDB data modeling different from data modeling with a relational
   database?

Output: 

.. code-block::

   When using a relational database:

   - You must determine a table's schema before you insert data. 
   - You often need to join data from several different tables to return the 
     data needed by your operation. 
   
   In MongoDB: 

   - Your schema can change over time as the needs of your application change.
   - The flexible data model lets you store data to match the way your 
     application returns data, and avoid joins. Avoiding joins across multiple 
     collections improves performance and reduces your deployment's workload.

Input: 

.. code-block::

   How can I combine multiple conditions in a single $search query?

Output:

.. code-block::

   To combine multiple conditions in a single $search query, use the "compound"
   operator. The "must" clause acts as an AND operator (all conditions must be met), 
   "should" increases the relevancy score for documents that match (acting as a 
   preferential OR), and "filter" applies conditions without affecting the score.
   For example:

   {
    "$search": {
     "compound": {
      "must": [
         {"text": {"query": "mongodb", "path": "title"} }
      ],
      "should": [
         {"text": {"query": "database", "path": "description"} },
         {"text": {"query": "flexibility", "path": "features"} }
      ],
      "filter": [
         {"range": {"path": "year", "gte": 2020 } } 
      ]
     }
    }
   }