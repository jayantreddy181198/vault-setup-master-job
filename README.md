# Vault Deployment on EKS

This repository contains a Kubernetes Job YAML file for setting up HashiCorp Vault on any Amazon EKS (Elastic Kubernetes Service) environment. The job automates the deployment of Vault and initializes it with essential configurations and policies.

## Prerequisites

Before you begin, ensure you have the following:

- An EKS cluster running and accessible.
- Helm installed on your local machine.
- kubectl configured to communicate with your EKS cluster.
- A PostgreSQL database running in the cluster for Vault storage.

## Job YAML Overview

The `vault-deploy-job.yaml` file contains the Kubernetes Job definition that:

1. Adds the HashiCorp Helm repository.
2. Pulls and installs the Vault Helm chart.
3. Creates a PostgreSQL role and database for Vault.
4. Sets up necessary Vault tables.
5. Initializes and unseals the Vault instance.
6. Configures Vault authentication methods and policies for Kubernetes and GitHub.

## Usage

1. Clone this repository:
   ```bash
   git clone <repository-url>
   cd <repository-name>
   ```

2. Modify the vault-deploy-job.yaml file:

    a. Replace $ns with the desired Kubernetes namespace.

    b. Adjust other parameters as needed.

3. Apply the Job to your EKS cluster:
    ```bash
    kubectl apply -f vault-deploy-job.yaml
    ```

4. Monitor the Job status:
    ```bash
    kubectl get jobs -n <namespace>
    ```

5. Once the Job completes successfully, the Vault instance will be running and unsealed.


### Accessing Vault

To access Vault, you can use the Vault CLI or API. Make sure to configure the necessary authentication methods (e.g., Kubernetes, GitHub) as specified in the Job.

### Cleanup

To remove the deployed resources, delete the Job and associated resources:


```bash
kubectl delete -f vault-deploy-job.yaml
```