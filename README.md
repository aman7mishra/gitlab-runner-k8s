# Running GitLab Runner on Kubernetes

Running GitLab Runner on Kubernetes is an efficient way to leverage the scalability and flexibility of Kubernetes while managing your CI/CD pipelines. Here's a guide to help you set up GitLab Runner on a Kubernetes cluster.

## Prerequisites

- **Kubernetes Cluster**: Ensure you have a running Kubernetes cluster. You can use managed Kubernetes services like GKE, EKS, or AKS, or set up your own using tools like Minikube.
- **kubectl**: Kubernetes command-line tool to interact with your cluster.
- **Helm**: Package manager for Kubernetes.
- **GitLab Account**: Access to your GitLab instance (either self-hosted or GitLab.com).

## Installation Steps

### Step 1: Clone the Repo

The following repo contains the `values.yaml`. We will use this file to provide custom values to the Helm chart.

### Step 2: Install Helm

If you haven't installed Helm, you can do so by following the official installation guide [here](https://helm.sh/docs/intro/install/).

### Step 3: Add GitLab Helm Repository

Add the GitLab repository to Helm:

```sh
helm repo add gitlab https://charts.gitlab.io/
helm repo update
```

### Step 4: Create a Namespace for GitLab Runner

It's a good practice to create a separate namespace for GitLab Runner:

```sh
kubectl create namespace gitlab-runner
```

### Step 5: Create a GitLab Runner Instance on GitLab

To register a new GitLab Runner, follow these steps:

**For GitLab.com:**

1. Go to your project or group in GitLab.
2. Navigate to **Settings > CI / CD**.
3. Expand the **Runners** section.
4. Click on **Register an instance runner/New group runner**.
5. Enter the Tags and other details. Leave the fields blank to use the default.
6. Copy the registration token provided.

**For Self-hosted GitLab:**

1. Log in to your GitLab instance.
2. Go to the desired project or group.
3. Navigate to **Settings > CI / CD**.
4. Expand the **Runners** section.
5. Click on **Register a Runner**.
6. Enter the Tags and other details. Leave the fields blank to use the default.
7. Copy the registration token provided.

**Note** - The code should begin with "glrt-"

### Step 6: Update the values.yaml

Update Tags and the service account name in the `values.yaml` file.

### Step 7: Install GitLab Runner using Helm

You can install the GitLab Runner Helm chart with the following command:

```sh
helm install --namespace gitlab-runner gitlab-runner -f values.yaml gitlab/gitlab-runner
```

Replace values.yaml with your custom configuration file. Refer to this documentation for more details.

## Conclusion
Running GitLab Runner on Kubernetes provides a scalable and flexible CI/CD environment that can handle large workloads efficiently. By using Helm, you can easily manage the deployment and configuration of GitLab Runner, ensuring that your pipelines run smoothly.
