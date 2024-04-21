# Argo CD GitOps Pipeline with Canary Rollouts

**This document outlines the steps to set up a GitOps pipeline for deploying and managing an application using Argo CD and implementing canary releases with Argo Rollouts.**

## Prerequisites

* A GitHub account with access to the `gh` CLI tool: https://cli.github.com/
* Docker installed: https://docs.docker.com/engine/install/
* A Kubernetes Cluster: https://kubernetes.io/docs/setup/
* Argo CD: https://argo-cd.readthedocs.io/en/stable/getting_started/
* Argo Rollouts: https://argo-rollouts.readthedocs.io/en/stable/installation/

## Task 1: Setup and Configuration

1. **Create a Git Repository & Upload your code for web-app to GitHub**
   - Login to GitHub using `gh auth login`.
   - Initialize a Git repository for your application code:
      ```bash
      git init
      git add .
      git commit -m "Initial commit"
      ```
   - Create a new repository on GitHub and push the local code:
      ```bash
      gh repo create Argo_CD --public --source=. --push
      ```

2. **Install Argo CD on Your Kubernetes Cluster**
   - Follow the steps outlined in the [Argo CD documentation](https://argo-cd.readthedocs.io/en/stable/getting_started/) to install Argo CD on the Kubernetes cluster.

3. **Install Argo Rollouts**
   - Installed Argo Rollouts on the Kubernetes cluster by following the steps provided in the [Argo Rollouts documentation](https://argo-rollouts.readthedocs.io/en/stable/installation/).

## Task 2: Creating the GitOps Pipeline

**Challenges:**

* Requires building and uploading a Docker image to a container registry.
* Automatic deploying changes from Git to k8s cluster.

**Steps:**

1. **Dockerize the Application** 
   - Build a Dockerfile for your weather application.
   - Use `docker build` to create the Docker image.
   - Push the image to a container registry (e.g., Docker Hub).

2. **Deploy the Application Using Argo CD**
   - Create a Kubernetes deployment manifest that uses the uploaded Docker image.
   - Deploy the application to Argo CD using `argocd app create` with the `--sync-policy automated` flag. This enables automatic deployment of changes from Git to the Kubernetes cluster.

## Task 3: Implementing a Canary Release with Argo Rollouts

**Challenges:**

* Requires defining a rollout strategy and monitoring the rollout process.

**Steps:**

1. **Define a Rollout Strategy**
   - Build a new Docker image for the canary version and upload it to Docker Hub.
   - Modify the Kubernetes deployment manifest to use the new Docker image and define a canary rollout strategy using Argo Rollouts.
   - Push changes to GitHub and wait for ArgoCD to deploy change to k8s cluster automatically.

2. **Trigger a Rollout**
   - Use Argo Rollouts to initiate the canary rollout.

3. **Monitor the Rollout**
   - Monitor the health and performance of the canary version during the rollout.

## Task 4: Cleanup

* Delete all argocd resources as a part of clean-up process.

