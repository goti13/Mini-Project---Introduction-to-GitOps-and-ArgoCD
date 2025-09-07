# Mini-Project---Introduction-to-GitOps-and-ArgoCD

Mini Project - Introduction to GitOps and ArgoCD


This project is focused on introducing the concept to GitOps using ArgoCD, specifically tailored for a Kubernetes environment hosted on AWS (Amazon Web Services). The project encompasses understanding GitOps principles, installing ArgoCD on an AWS-managed Kubernetes cluster, and exploring ArgoCD's architecture and components.


Pre-requisites


1. Basic Understanding of Kubernetes

- Familiarity with Kubernetes concepts such as pods, deployments, and services.

- Resource: [Kubernetes Basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/).

2. [AWS Account](https://repost.aws/knowledge-center/create-and-activate-aws-account)

- An active AWS account to create and manage an Amazon EKS cluster.

- Sign Up: AWS Account Creation.

3. Amazon EKS Cluster

- A running EKS (Elastic Kubernetes Service) cluster.

- Installation Guide: [Creating an Amazon EKS Cluster](https://docs.aws.amazon.com/eks/latest/userguide/create-cluster.html)

- Tools: AWS Management Console or AWS CLI for cluster management.

4. kubectl

- Command-line tool for interacting with the Kubernetes cluster.

- Installation Guide: [Install and Set Up kubectl](https://kubernetes.io/docs/tasks/tools/).

5. AWS CLI

- command-line tool for managing AWS services.

- Installation Guide: [Installing AWS CLI](https://aws.amazon.com/cli/).

6. Git

-  Version control system to manage source code.

- Installation Guide: [Git Installation](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).



7. ArgoCD

- Understanding of ArgoCD's basic concepts and its role in GitOps.

-  ArgoCD Documentation: [ArgoCD - GitOps for Kubernetes](https://argo-cd.readthedocs.io/en/stable/).

8. Text Editor/IDE

- A text editor or Integrated Development Environment (IDE) for editing code and configuration files.

- Options include Visual Studio Code (VSCode), Sublime Text, Atom, etc.

-  VSCode: [Download Visual Studio Code](https://code.visualstudio.com/download).

9. Docker (Optional but Recommended)

- For building and managing containers, if the project includes working with containerized applications.

- Installation Guide: [Docker Installation](https://code.visualstudio.com/download).

10. Helm and Kustomize (Optional)

- Tools for managing Kubernetes packages and customizing Kubernetes object configurations.

- Helm Installation: [Installing Helm](https://helm.sh/docs/intro/install/).

- Kustomize Installation: [Installing Kustomize](https://kubectl.docs.kubernetes.io/installation/kustomize/).

11. Internet Connection

-  Stable internet connection for accessing AWS services, online documentation, and forums.

12. Hardware Requirements

- A computer with sufficient RAM (at least 8GB recommended) and processing power to handle virtualization if necessary.




Lesson 1.1: GitOps Principles and the Role of ArgoCD

Objective: Understand GitOps principles and ArgoCD's role in Kubernetes.

Lesson 1.1: GitOps Principles and the Role of ArgoCD

Objective

To gain a comprehensive understanding of GitOps principles and the pivotal role of ArgoCD in implementing these principles within a Kubernetes environment.

1. Study GitOps Principles:
- Key Concepts: Explore the fundamental concepts of GitOps including:
	- Infrastructure as Code (IaC): Understand how infrastructure is managed and provisioned  through code, rather than manual processes.
	- Automated Deployment: Learn about the automated processes that ensure deployments are consistent and repeatable.
	- Merge Requests for Change Management: Discover how changes are reviewed and merged, ensuring a controlled and traceable approach to         environment modific


Benefits of GitOps:

- Enhanced Developer Productivity: Due to automated, predictable deployments.

- Improved Stability: As the entire system state is version-controlled.

- Easier Recovery: The ability to revert to a previous state is simplified.

-  Recommended Reading: For a deeper dive, explore the Weaveworks GitOps Principles. This resource provides an in-depth look at the            principles, practices, and benefits


2. Role of ArgoCD in GitOps:

- Automating Kubernetes Deployments:
	- Understand how ArgoCD automates the deployment of applications to Kubernetes clusters by monitoring Git repositories.
	- ArgoCD continuously compares the desired application state in Git with the live state in Kubernetes, ensuring consistency.

- Features of ArgoCD:

	- Declarative Setup: ArgoCD uses a declarative approach for infrastructure and application deployment.
	- Self-healing: Automatic correction of detected drifts in the desired and live states.

	- Multi-Cluster Management: Manage deployments across multiple Kubernetes clusters.

	- Integration with Various Tools: Works with Helm, Kustomize, and others for configuration management.

- Use Cases:

	- Illustrate common scenarios where ArgoCD provides significant advantages, such as multi-environment deployments and rollbacks.

   
- ArgoCD Documentation: [Review the ArgoCD - GitOps for Kubernetes](https://argo-cd.readthedocs.io/en/stable/) for detailed insights into     its functionalities, installation, and usage.



Lesson 1.2: Installing and Configuring ArgoCD in an AWS Kubernetes Environment


Objective: Install ArgoCD on an EKS (Elastic Kubernetes Service) cluster on AWS.

Steps:

1. Set Up an EKS Cluster:

- Use AWS Management Console or AWS CLI to create an EKS cluster.

- Follow the AWS Guide: [Creating an Amazon EKS Cluster](https://docs.aws.amazon.com/eks/latest/userguide/create-cluster.html).

<img width="1211" height="449" alt="image" src="https://github.com/user-attachments/assets/f29b76ac-08f8-40ee-843a-4b3623182ef1" />

<img width="2392" height="850" alt="image" src="https://github.com/user-attachments/assets/62231cea-af1c-45d3-9b75-d4708bce6d4e" />

<img width="2336" height="752" alt="image" src="https://github.com/user-attachments/assets/32bca6c8-fcb9-47be-90a8-e9a147ec1270" />

<img width="1532" height="222" alt="image" src="https://github.com/user-attachments/assets/2c63b1db-d837-41b8-bf83-18d16b445ef8" />
















2. Install ArgoCD on EKS:


- Apply the ArgoCD installation manifest using kubectl.

- Code Snippet:


```

kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

```

<img width="1570" height="176" alt="image" src="https://github.com/user-attachments/assets/1a46b760-cad7-426d-ac64-eae618fa47dd" />

<img width="2416" height="902" alt="image" src="https://github.com/user-attachments/assets/3b0a875f-723d-42f1-8e17-7fc76ced1753" />

<img width="2416" height="880" alt="image" src="https://github.com/user-attachments/assets/30bb6d27-2955-4c7e-ad42-d64fadc35db3" />

<img width="1884" height="312" alt="image" src="https://github.com/user-attachments/assets/2df0e332-e85a-48b5-834a-5f4333a22322" />




- Explanation: This code snippet creates a namespace for ArgoCD and then applies the ArgoCD manifests to the EKS cluster.

- The namespace isolates ArgoCD resources.



3. Access ArgoCD UI on EKS:

Option 1: Port-Forwarding (Temporary Access)

- Use kubectl port-forwarding or set up an Ingress controller to access the ArgoCD Ul.

- Code Snippet for Port Forwarding


```

kubectl port-forward svc/argocd-server -n argocd 8080:443


```

Access the UI at https://localhost:8080 (ignore SSL warnings).

	
- Explanation: This forwards port 8080 of your local machine to port 443 of the ArgoCD server, allowing access via ' localhost: 8080'.

Option 2: LoadBalancer (Permanent Access)

```

kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'

```
- Get the LoadBalancer URL:


```

kubectl get svc argocd-server -n argocd -o jsonpath='{.status.loadBalancer.ingress[0].hostname}'

```

- Access the UI via the provided URL (e.g., https://<loadbalancer-url>)


- Retrieve Admin Password

  
The default username is admin. Retrieve the password:

```

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

```

<img width="1205" height="189" alt="image" src="https://github.com/user-attachments/assets/1f942fec-37a1-4692-a36d-eaf5c9b504f6" />


<img width="2880" height="1608" alt="image" src="https://github.com/user-attachments/assets/487c164e-17da-4156-a77e-99957639b231" />



Lesson 1.3: ArgoCD Architecture: Understanding Core Components

Objective: Get acquainted with ArgoCD's architecture in the context of AWS.

Steps:

1. Explore ArgoCD Components:


- Understand the functions of the API Server, Repository Server, and Application Controller.


- ArgoCD consists of several key components:

API Server: Handles UI/CLI interactions and authentication.

Repository Server: Stores and manages Git repositories containing manifests.

Application Controller: Monitors applications and ensures desired state matches live state.

Redis: Caches data for performance.

Dex Server: Integrates with SSO for authentication (if configured) 25.

View the deployed components:

2. Navigate ArgoCD Ul:

-  Familiarize yourself with viewing applications, managing repositories, and monitoring deployments through the ArgoCD Ul.

- Navigate ArgoCD UI
- 
Explore the UI features:

Applications: View deployed apps and their sync status.

Settings > Repositories: Add private Git repositories (e.g., GitHub, AWS CodeCommit).

Projects: Manage team access and permissions.

Cluster Management: Register external clusters (if needed) 

3. Deploy a Sample Application:

- Use a public Git repository with Kubernetes manifests to deploy an application via ArgoCD.

- Follow the ArgoCD guide: Deploying Applications.

Use a public Git repository (e.g., ArgoCD examples) to deploy a sample app:

Using CLI:

The ArgoCD CLI (argocd) is required to interact with ArgoCD from your terminal. Here's how to install

```
brew install argocd
```
- Login to the ArgoCD Server

Retrieve the Admin Password

The default username is admin. Get the password:

```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

```

- Login via CLI


Use the argocd login command with the server address:

If using port forwarding (localhost):

```
argocd login localhost:8080 --insecure --username admin --password <YOUR_PASSWORD>

```

If using LoadBalancer (external IP):

First get the LoadBalancer URL then login:

```

kubectl get svc argocd-server -n argocd -o jsonpath='{.status.loadBalancer.ingress[0].hostname}'

```

```
argocd login <EXTERNAL-IP> --insecure --username admin --password <YOUR_PASSWORD>

```
<img width="1193" height="57" alt="image" src="https://github.com/user-attachments/assets/aea83a35-129c-4c9b-8f2f-50efdb5a8710" />

If using Ingress (domain):

```
argocd login your-argocd-domain.com --insecure --username admin --password <YOUR_PASSWORD>

```
Creating the Application

```

argocd app create guestbook \
  --repo https://github.com/argoproj/argocd-example-apps.git \
  --path guestbook \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace default

```
<img width="1215" height="181" alt="image" src="https://github.com/user-attachments/assets/e8936818-10ef-4566-9098-b1dcb47de1fd" />

Using UI:
Click "+ New App."

Fill in:

Application Name: guestbook

Project: default

Repository URL: https://github.com/argoproj/argocd-example-apps.git

Path: guestbook

Cluster URL: https://kubernetes.default.svc

Namespace: default

Click "Create" 




4. Monitor Synchronization:


- Observe how ArgoCD syncs the desired state from the Git repository to the EKS cluster.

ArgoCD automatically syncs the application. Check status:

```

argocd app get guestbook

```

CLI:

```
argocd app get guestbook

```
<img width="1790" height="516" alt="image" src="https://github.com/user-attachments/assets/54483c48-b3bf-4c18-a978-6c0dec52f01e" />


UI:
View the application health and sync status.

Click on the app to see resources (pods, services, etc.).

<img width="2794" height="1238" alt="image" src="https://github.com/user-attachments/assets/9a7dbe85-c284-4025-ba70-38e802c39e56" />



Trigger a Manual Sync (if not automated):

```
argocd app sync guestbook

```

Enable Auto-Sync (for automatic drift detection and correction):

```
argocd app set guestbook --sync-policy automated

```
<img width="1822" height="100" alt="image" src="https://github.com/user-attachments/assets/af4de11a-d074-4c6f-95d6-625deb0afc48" />


<img width="1416" height="674" alt="image" src="https://github.com/user-attachments/assets/99488b30-644d-444d-9c52-2a22e1cd814e" />


Example Application Manifest for GitOps

Create a YAML file (e.g., my-app.yaml) to manage applications declaratively:


```
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: my-app
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://github.com/your-repo/manifests.git
    targetRevision: HEAD
    path: dev  # Directory in repo
  destination:
    server: https://kubernetes.default.svc
    namespace: my-app-namespace
  syncPolicy:
    automated:
      selfHeal: true  # Auto-correct drift
      prune: true     # Delete removed resources
    syncOptions:
    - CreateNamespace=true  # Auto-create namespace

```

Apply it:

```
kubectl apply -f my-app.yaml

```

💡 Best Practices for GitOps with ArgoCD

- Use Private Repositories: Secure your manifests using SSH keys or HTTPS credentials.

- Enable SSL/TLS: Configure HTTPS for ArgoCD server using Ingress or LoadBalancer.

- Implement RBAC: Restrict access to ArgoCD resources using roles and projects.

- Monitor Drift: Use automated sync with selfHeal and prune to enforce state.

- Avoid Manual Changes: All changes should be committed to Git to prevent drift

🧹 Cleanup


```

# Delete ArgoCD application
argocd app delete guestbook

# Uninstall ArgoCD
kubectl delete -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Delete EKS cluster
eksctl delete cluster --name my-argocd-cluster --region us-east-1

```

<img width="2404" height="958" alt="image" src="https://github.com/user-attachments/assets/a862883a-b417-47e9-b0f3-ec8ebfbbda4b" />


<img width="2368" height="928" alt="image" src="https://github.com/user-attachments/assets/95ef69f2-d159-4239-868a-02295d83b053" />










