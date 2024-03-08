  .. step:: Provide |idp-provider| credentials to |service|.

     .. procedure::
	:style: connected

	.. step:: Click :guilabel:`Identity Providers` in the 
	   left-hand pane. If you have previously configured an |idp|,
	   click :guilabel:`Add Identity Provider` in the upper-right 
	   corner of the page, then click 
	   :guilabel:`Setup Identity Provider`. If you have not 
	   previously configured an |idp|, click 
	   :guilabel:`Setup Identity Provider`.

	.. step:: On the :guilabel:`Configure Identity Provider` 
	   screen, enter the following information:

	   .. list-table::
	      :widths: 20 40
	      :header-rows: 1

	      * - Field
		- Value

	      * - :guilabel:`Configuration Name`
		- Descriptive label that identifies the configuration

	      * - :guilabel:`Issuer URI`
		- :guilabel:`Fill with Placeholder Values`

	      * - :guilabel:`Single Sign-On URL`
		- :guilabel:`Fill with Placeholder Values`

	      * - :guilabel:`Identity Provider Signature Certificate`
		- Certificate you received from |idp-provider|
		  in a prior step

	      * - :guilabel:`Request Binding`
		- ``HTTP POST``

	      * - :guilabel:`Response Signature Algorithm`
		- ``SHA-256``

	.. step:: Click the :guilabel:`Next` button to see the values
	   for the |idp-provider| configuration.

	.. step:: Click :guilabel:`Finish`.
