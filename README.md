## Azure DevOps Agent Docker Image

This repository contains a Dockerfile for building an Azure DevOps agent image that can be deployed to a Kubernetes cluster as a pod.
It also contains a pipeline to build and deploy the Agents Docker images to ECR.

It's worth noting that I modified the original Dockerfile and startup script to add more tools that didn't exist and the ability to pass a custom capability to the Agent when created. 

To make it easier, I organized the files and folders needed for you to have everything required.
For instance, I’ve created a directory named python38 that represents an Azure DevOps Docker Agent Docker image for Python 3.8, which can be helpful when moving Python-based CI pipelines and automation tests to Kubernetes.
This just one example.

My solution uses a different Docker image for each framework I need for my CI pipelines.
We can always add more for frameworks like Java, Dotnet, and Robot Framework, among others. Each framework will contain a Dockerfile that will be based on the generic Docker image that is built using the pipeline, and will include all the SDK and tools that it needs to compile or test the code.


### Prerequisites

Before building the Docker image, you'll need to set up the following:

- An Amazon Web Services (AWS) account and Elastic Container Registry (ECR) repository.
- An Azure DevOps account and personal access token (PAT).
- A Kubernetes cluster where you'll deploy the agent as a pod.

### Building the Docker Image

The `azure-pipelines.yaml` file in the root directory of the repository contains a pipeline that automatically builds the Docker image and pushes it to your ECR repository.

The pipeline will bump the patch version number in the `VERSION` file for each run. You can customize the agent version by modifying this file.

To start the pipeline, create a new build in Azure DevOps and select the `azure-pipelines.yaml` file as the pipeline configuration.

### Deploying the Agent

Once you've built the Docker image and pushed it to your ECR repository, you can deploy it to your Kubernetes cluster using the Helm chart in the `azdo-agents-gitops` repository.

To deploy the agent, clone the `azdo-agents-gitops` repository and follow the instructions in the README file.

Note that the Helm chart uses the Docker image version number as set in the `VERSION` file, so make sure to update the version number in this file before deploying a new version of the agent.

### Conclusion

This repository provides a convenient way to build and deploy an Azure DevOps agent to a Kubernetes cluster as a pod. With the pipeline and Helm chart, you can automate the build and deployment process and easily update the agent version as needed. ArgoCD can be used to automatically deploy the new version of the agent when the Helm chart version changes.
