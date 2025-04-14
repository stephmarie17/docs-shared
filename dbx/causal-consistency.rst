MongoDB enables **causal consistency** in certain client
sessions. The causal consistency model guarantees that in a
distributed system, operations within a session run in a causal
order. Clients observe results that are consistent
with the causal relationships, or the dependencies between
operations. For example, if you perform a series of operations where
one operation logically depends on the result of another, any subsequent
reads reflect the dependent relationship.

To guarantee causal consistency, client sessions must fulfill the
following requirements:

- When starting a session, the driver must enable the causal consistency
  option. This option is enabled by default.

- Operations must run in a single session on a single thread. Otherwise,
  the sessions or threads must communicate the operation time and cluster
  time values to each other. To view an example of two sessions that communicate
  these values, see the :manual:`Causal Consistency examples </core/read-isolation-consistency-recency/#examples>`
  in the {+mdb-server+} manual.

- You must use a |majority-rc| read concern.

- You must use a |majority-wc| write concern. This is the default write concern
  value.
  
The following table describes the guarantees that causally
consistent sessions provide:

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - Guarantee
     - Description

   * - Read your writes
     - Read operations reflect the results of preceding write operations.

   * - Monotonic reads
     - Read operations do not return results that reflect an earlier data state than
       a preceding read operation.

   * - Monotonic writes
     - If a write operation must precede other write operations, the server
       runs this write operation first.

       For example, if you call |insert-one-method| to insert a document, then call
       |update-one-method| to modify the inserted document, the server runs the 
       insert operation first.

   * - Writes follow reads
     - If a write operation must follow other read operations, the server runs
       the read operations first.

       For example, if you call |find-one-method| to retrieve a document, then call
       |delete-one-method| to delete the retrieved document, the server runs the find
       operation first.

.. tip::

   To learn more about the concepts mentioned in this section, see the 
   following {+mdb-server+} manual entries:

   - :manual:`Causal Consistency </core/read-isolation-consistency-recency/#causal-consistency>`
   - :manual:`Causal Consistency and Read and Write Concerns </core/causal-consistency-read-write-concerns/>`