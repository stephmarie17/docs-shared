To use DNS service discovery to look up the DNS SRV record of the service you're connecting to,
specify the SRV connection format in your connection string. Additionally, if you enable
the SRV connection format, the {+driver-short+} automatically re-scans for new hosts without
having to change the client configuration.

The following code shows a connection string that uses the SRV connection format:

|srv-uri|

To learn more about the SRV connection format, see the :manual:`SRV Connection Format </reference/connection-string/#std-label-connections-dns-seedlist>`
entry in the {+mdb-server+} manual.