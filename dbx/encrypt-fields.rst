=================
In-Use Encryption
=================

.. contents:: On this page
   :local:
   :backlinks: none
   :depth: 2
   :class: singlecol

Overview
--------

You can encrypt fields in a document using a set of features called
**in-use encryption**.

In-use encryption enables your client applications to encrypt data
*before* sending it to MongoDB, and to query documents with encrypted fields.

Because the driver encrypts the data before sending it to MongoDB, only
your configured client applications can decrypt the data. Only applications
using the driver with access to your encryption keys can access the decrypted,
plaintext data. Should you have unauthorized access to your database, an
attacker could only see the encrypted, ciphertext data.

In-use encryption can help prevent exposure of the following sensitive types of data:

- Credit card numbers
- Addresses
- Health information
- Financial information
- Any other sensitive or personally identifiable information (PII)

MongoDB offers the following ways to encrypt fields:

Queryable Encryption
~~~~~~~~~~~~~~~~~~~~

Queryable Encryption is the next-generation in-use encryption feature,
introduced in MongoDB Server version 6.0 and available as a public
preview. Queryable Encryption supports searching encrypted fields for
equality and encrypts each value uniquely.

The MongoDB manual contains detailed information on the following Queryable Encryption topics:

- To get started, see the :ref:`Queryable Encryption Quick Start <qe-quick-start>`.
- To learn how to use Queryable Encryption, see the :ref:`Queryable Encryption Fundamentals <qe-fundamentals>`.
- To learn how to integrate your implementation with a Key Management System, see the :ref:`Queryable Encryption Tutorials <qe-tutorials>`.
- To learn Queryable Encryption concepts, see the :ref:`Queryable Encryption Reference <qe-reference>`.

Client-side Field Level Encryption
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Client-side Field Level Encryption (CSFLE) was introduced in MongoDB
Server version 4.2 and supports searching encrypted fields for equality.
CSFLE differs from Queryable Encryption in that it requires that the encrypted fields
you want to search must be deterministically encrypted. When you
deterministically encrypt a value, the same input value produces the
same output value. While deterministic encryption provides greater 
support for read operations, encrypted data with low :wikipedia:`cardinality <Cardinality>`
is susceptible to recovery using :wikipedia:`frequency analysis <Frequency_analysis>`.

The MongoDB manual contains detailed information on the following CSFLE topics:

- To get started, see the :ref:`CSFLE Quick Start <csfle-quick-start>`.
- To learn how to use CSFLE, see the :ref:`CSFLE Fundamentals <csfle-fundamentals>`.
- To learn how to integrate your CSFLE implementation with a Key Management System, see the :ref:`CSFLE Tutorials <csfle-tutorials>`.
- To learn CSFLE concepts, see the :ref:`CSFLE Reference <csfle-reference>`.
