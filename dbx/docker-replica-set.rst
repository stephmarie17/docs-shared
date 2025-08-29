When a replica set runs in Docker, it might expose only one MongoDB endpoint.
In this case, the replica set is not discoverable. Specifying ``directConnection=false`` in your connection URI,
or leaving this option unset, can prevent your application from connecting to it.

In a test or development environment, you can connect to the replica set by specifying
``directConnection=true``. In a production environment, we
recommend configuring the cluster to make each MongoDB instance accessible outside of
the Docker virtual network.