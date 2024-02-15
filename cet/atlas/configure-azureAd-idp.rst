To register your |oidc| or OAuth application with Microsoft Entra ID:

.. procedure::
   :style: normal

   .. step:: Register an application.

      .. procedure::
         :style: connected

         .. step:: Navigate to :guilabel:`App registrations`.
            
            .. procedure::
               :style: connected

               .. step:: In your `Azure portal <https://portal.azure.com/>`__ account, search and click :guilabel:`Microsoft Entra ID`.

               .. step:: In the :guilabel:`Manage` section of the left navigation, click :guilabel:`App registrations`.
         
         .. step:: Click :guilabel:`New registration`.

         .. step:: Apply the following values.

            .. list-table::
               :header-rows: 1
               :widths: 20 40

               * - Field
                 - Value

               * - :guilabel:`Name`
                 - :guilabel:`Atlas Database - OIDC`

               * - :guilabel:`Supported Account Types`
                 - :guilabel:`Accounts in this organizational directory only (single tenant)`

               * - :guilabel:`Redirect URI`
                 - | - :guilabel:`Public client/native (mobile & desktop)`
                   | - ``http://localhost:27097/redirect``

         .. step:: Click :guilabel:`Register`.

      To learn more about registering an application, see `Azure Documentation <https://learn.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app#register-an-application>`__.

   .. step:: Add a group claim.

      .. procedure::
         :style: connected

         .. step:: Navigate to :guilabel:`Token Configuration`.

            In the :guilabel:`Manage` section of the left navigation,
            click :guilabel:`Token Configuration`.

         .. step:: Click :guilabel:`Add groups claim`.

         .. step:: In the :guilabel:`Edit groups claim` modal, select :guilabel:`Security`.

            What groups you select depend on the type of groups you configured
            in your Azure environment. You may need to select a different
            type of group to send the appropriate group information.

         .. step:: In the :guilabel:`Customize token properties by type` section, ensure that you only select :guilabel:`Group ID`.

            When you select :guilabel:`Group Id`, Azure sends the
            security group's Object ID.

         .. step:: Click :guilabel:`Add`.

      To learn more about adding a group claim, see `Azure Documentation <https://learn.microsoft.com/en-us/azure/active-directory/hybrid/connect/how-to-connect-fed-group-claims>`__.

   .. step:: Add a user identifier claim to the access token.

      .. procedure::
         :style: connected

         .. step:: Click :guilabel:`Add optional claim`.

         .. step:: In the :guilabel:`Add optional claim` modal, select :guilabel:`Access`.
         
         .. step:: Select a claim that carries a user identifier that you can
            refer to in MongoDB access logs such as an email.
         
         .. step:: Click :guilabel:`Add`.
         
         .. step:: In the :guilabel:`Microsoft Graph Permissions` note, check the box, and click :guilabel:`Add`.

      To learn more, see `Azure Documentation <https://learn.microsoft.com/en-us/azure/active-directory/develop/optional-claims>`__.

   .. step:: Update the manifest.

      .. procedure::
         :style: connected

         .. step:: In the :guilabel:`Manage` section of the left navigation, click :guilabel:`Manifest`.

         .. step:: Update the :guilabel:`accessTokenAcceptedVersion` from ``null`` to ``2``.

            The number ``2`` represents Version 2 of Microsoft's access
            tokens. Other applications can use this as a signed
            attestation of the Active Directory-managed user's identity.
            Version 2 ensures that the token is a JSON Web Token that
            MongoDB understands.
         
         .. step:: Click :guilabel:`Save`.

      To learn more about adding an optional claim, see `Azure Documentation <https://learn.microsoft.com/en-us/azure/active-directory/develop/reference-app-manifest>`__.

   .. step:: Remember metadata.

      .. procedure::
         :style: connected

         .. step:: In the left navigation, click :guilabel:`Overview`.
         
            Copy the :guilabel:`Application (client) ID` value.
 
         .. step:: In the top navigation, click :guilabel:`Endpoints`.
            
            Copy the :guilabel:`OpenID Connect metadata document` value 
            without the ``/.well-known/openid-configuration`` part.

            You can also retrieve this value by following the
            :guilabel:`OpenID Connect metadata document` |url| and
            copying the value for ``issuer``.

      The following table shows what these Microsoft Entra ID UI values map to in our |service| Configuration Properties:
      
      .. list-table::
         :header-rows: 1
         :widths: 50 50
         :stub-columns: 1

         * - Microsoft Entra ID UI 
           - |service| Configuration Property

         * - :guilabel:`Application (client) ID` 
           - | :guilabel:`Client ID`
             | :guilabel:`Audience`

         * - :guilabel:`OpenID Connect metadata document (without /.well-known/openid-configuration)`
           - :guilabel:`Issuer URI`. 
