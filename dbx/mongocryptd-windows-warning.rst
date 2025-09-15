.. warning:: MongoDB 8.2 Known Issue

   Version 8.2.0 of ``mongocryptd`` might not run on Windows.
   This bug affects encryption with the driver if you
   specify the ``--logpath NUL`` argument when starting
   ``mongocryptd``.

   To learn more about this issue and how to resolve it, see :ref:`8.2-known-issues`
   in the MongoDB 8.2 Release Notes.