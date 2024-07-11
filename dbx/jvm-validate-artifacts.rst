===================================
Validate Driver Artifact Signatures
===================================

.. facet::
   :name: genre
   :values: tutorial

.. meta::
   :keywords: java, kotlin, security, SSDLC

.. contents:: On this page
   :local:
   :backlinks: none
   :depth: 1
   :class: singlecol

Overview
--------

You can validate the signature of a {+driver-short+} artifact published
on Maven. This process can enhance the security of your system or
network by allowing you to confirm the authenticity of the driver.

Procedure
---------

The following steps describe how you can validate driver artifact
signatures.

.. procedure::
   :style: normal

   .. step:: Install an Encryption Software
      
      You must first install one of the following encryption suites:
      
      - `GnuPG <https://gnupg.org/>`__ (`Homebrew Installation <https://formulae.brew.sh/formula/gnup>`__)
      - `GPG Suite <https://gpgtools.org>`__ (`Homebrew Installation <https://formulae.brew.sh/cask/gpg-suite>`__)

   .. step:: Download and Import the Public Key
      
      Navigate to the driver source GitHub repository and view
      the `Releases <https://github.com/mongodb/mongo-java-driver/releases>`__ page.
      Each version release contains instructions on how to download and import the public key for
      verifying signatures.

   .. step:: Download the Signed File

      In your terminal, run a ``curl`` command to download the signed
      file corresponding to a version of the driver. For example,
      running the following command downloads the signed file for the
      v5.1.0 driver:

      .. code-block:: sh
      
         curl -LO https://repo.maven.apache.org/maven2/org/mongodb/mongodb-driver-core/5.1.0/mongodb-driver-core-5.1.0.jar

   .. step:: Download the File Signature
      
      In your terminal, run a ``curl`` command to download the file
      signature corresponding to a version of the driver. For example,
      running the following command downloads the file signature for the
      v5.1.0 driver:

      .. code-block:: sh

         curl -LO https://repo.maven.apache.org/maven2/org/mongodb/mongodb-driver-core/5.1.0/mongodb-driver-core-5.1.0.jar.asc

   .. step:: Verify the Signature
      
      Finally, you can verify the signature by using the encryption package.
      The following terminal command uses ``gpg`` to verify the artifact signature of the v5.1.0
      driver:

      .. code-block:: sh

         gpg --verify mongodb-driver-core-5.1.0.jar.asc mongodb-driver-core-5.1.0.jar
      
      If you successfully verify the signature, you see a message
      similar to the following:

      .. code-block:: none
         :copyable: false

         gpg: Signature made Tue 30 Apr 12:05:34 2024 MDT
         gpg:                using RSA key 76E0008D166740A8
         gpg: Good signature from "MongoDB Java Driver Release Signing Key <packaging@mongodb.com>" [unknown]
         gpg: WARNING: This key is not certified with a trusted signature!
         gpg:          There is no indication that the signature belongs to the owner.
         Primary key fingerprint: 1A75 005E 1421 9222 3D6A  7C3B 76E0 008D 1667 40A8

Additional Information
----------------------

To learn more about verifying signatures, see :manual:`Verify Integrity
of MongoDB Packages </tutorial/verify-mongodb-packages/>` in the Server
manual.

To learn more about GnuPG, see the `GNU Privacy Handbook
<https://gnupg.org/gph/en/manual/book1.html>`__.
