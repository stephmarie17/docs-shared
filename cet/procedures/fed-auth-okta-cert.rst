.. procedure::
   :style: normal

   .. step:: Download your |idp-provider| origination 
      certificate.
      
      .. procedure:: 
         :style: connected

         .. step:: In your |idp-provider| account, click
            :guilabel:`Admin` in the upper right corner to access
            the Administrator environment.

         .. step:: In the left-hand pane, navigate to 
            :guilabel:`Applications` -> :guilabel:`Applications`.

         .. step:: Click :guilabel:`Create App Integration`.
            Select :guilabel:`SAML 2.0` for the 
            :guilabel:`Sign-in method` and click
            :guilabel:`Next`.

         .. step:: Fill in the :guilabel:`App name` text field with
            your desired application name.

         .. step:: Optionally, add a logo image and set app 
            visibility. Click :guilabel:`Next`.

         .. step:: On the :guilabel:`Configure SAML` screen, enter the
            following information:

            .. list-table::
               :widths: 20 40
               :header-rows: 1

               * - Field
                 - Value

               * - :guilabel:`Single sign-on URL`
                 - ``http://localhost``

               * - :guilabel:`Audience URI`
                 - ``urn:idp:default``
            
            .. important::
              
               These are placeholder values and are **not** intended
               for use in production. You will replace them in a later
               step.

            Leave the other fields empty or set to their default values
            and click :guilabel:`Next` at the bottom of the page.

         .. step:: On the :guilabel:`Feedback` screen, select
            :guilabel:`I'm an Okta customer adding an internal app` and
            click :guilabel:`Finish`.

         .. step:: At the bottom of the page under the heading
            :guilabel:`SAML Signing Certificates`, locate the newest
            certificate with a :guilabel:`Status` of ``Active``--this 
            is the certificate you just created.

            Click :guilabel:`Actions` and select 
            :guilabel:`Download certificate` from the drop-down menu.
            The generated certificate is a ``.cert`` file. You must
            convert it to a ``.pem`` certificate for use later in this
            procedure. To do this, open a terminal of your choosing and
            run the following:

            .. code-block:: sh

               openssl x509 -in path/to/mycert.crt -out path/to/mycert.pem -outform PEM 
