.. step:: Replace placeholder values in the |service| 
   |fmc|.

   .. procedure::
      :style:connected

      .. step:: On the Okta application page, click
	 :guilabel:`View Setup Instructions`
	 in the middle of the page.

      .. step:: In the |service| |fmc|, navigate to the
	 :guilabel:`Identity Providers` page. Locate your
	 |idp-provider| and click :guilabel:`Edit`.

      .. step:: Replace the placeholder values in the following
	 fields:

	 .. list-table::
	    :widths: 20 40
	    :header-rows: 1

	    * - FMC Data Field
	      - Value

	    * - :guilabel:`Issuer URI`
	      - :guilabel:`Identity Provider Issuer` value from
		the Okta Setup Instructions page.

	    * - :guilabel:`Single Sign-on URL`
	      - :guilabel:`Identity Provider Single Sign-On URL`
		value from the Okta Setup Instructions page.

	    * - :guilabel:`Identity Provider Signature Certificate`
	      - Copy the :guilabel:`X.509 Certificate` from the 
		Okta Setup Instructions page and paste the contents
		directly.

      .. step:: Click :guilabel:`Next`.

      .. step:: Click :guilabel:`Finish`.

.. step:: Assign users to your |idp-provider| 
   application.

   .. procedure::
      :style:connected

      .. step:: On the Okta application page, click the
	 :guilabel:`Assignments` tab.

      .. step:: Ensure that all your |service| organization users
	 who will use Okta are enrolled.
