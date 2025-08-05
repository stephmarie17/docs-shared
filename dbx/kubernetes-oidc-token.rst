If you specify Kubernetes OIDC as the authentication mechanism, the driver reads
the contents of the OIDC token from one of the following locations:

- ``AZURE_FEDERATED_TOKEN_FILE`` environment variable for applications running
  on `Azure Kubernetes Service (AKS)
  <https://azure.microsoft.com/en-us/products/kubernetes-service>`__
- ``AWS_WEB_IDENTITY_TOKEN_FILE`` environment variable for applications running
  on `Elastic Kubernetes Service (EKS) <https://aws.amazon.com/eks/>`__
- ``/var/run/secrets/kubernetes.io/serviceaccount/token`` file, the default
  location for all other applications, including ones that run on `Google
  Kubernetes Engine (GKE) <https://cloud.google.com/kubernetes-engine>`__

You must store your OIDC token in the location that corresponds to the service
you use to run your application.