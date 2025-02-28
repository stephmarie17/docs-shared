MongoDB enables **causal consistency** in client sessions.
The causal consistency model guarantees that operations within a session
run in a causal order. Clients observe results that are consistent
with the causal relationships, or the dependencies between
operations. For example, if you perform a series of operations where
one operation logically depends on the result of another, any subsequent
reads reflect the dependent relationship.

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
     - If a write operation must precede other write operations, the driver
       runs this write operation first.

       For example, if you call |insert-one-method| to insert a document, then call
       |update-one-method| to modify the inserted document, the driver runs the 
       insert operation first.

   * - Writes follow reads
     - If a write operation must follow other read operations, the driver runs
       the read operations first.

       For example, if you call |find-one-method| to retrieve a document, then call
       |delete-one-method| to delete the retrieved document, the driver runs the find
       operation first.

In a causally consistent session, MongoDB ensures a
causal relationship between the following operations:

- Read operations that have a |majority-rc| read concern
- Write operations that have a |majority-wc| write concern

.. tip::

   To learn more about the concepts mentioned in this section, see the 
   following {+mdb-server+} manual entries:

   - :manual:`Causal Consistency </core/read-isolation-consistency-recency/#causal-consistency>`
   - :manual:`Causal Consistency and Read and Write Concerns </core/causal-consistency-read-write-concerns/>`