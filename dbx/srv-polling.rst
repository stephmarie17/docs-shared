To use DNS service discovery to look up the DNS SRV record of the service you're connecting to,
specify the SRV connection format in your connection string. If you specify this format,
the {+driver-short+} automatically rescans for new hosts. Your deployment can add hosts to its
topology without requiring changes in your client configuration.

The following code shows a connection string that uses the SRV connection format:

|srv-uri|

To learn more about the SRV connection format, see the :manual:`SRV Connection Format </reference/connection-string/#std-label-connections-dns-seedlist>`
entry in the {+mdb-server+} manual.