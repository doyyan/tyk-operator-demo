# tyk-operator-demo

A practical example demonstrating how to implement a GitOps workflow using **Tyk Operator**, **ArgoCD**, and **Kustomize** to manage API deployments across multiple Kubernetes environments.

## About
In this repo, we walk through setting up a GitOps workflow that automates the deployment of both applications and API configurations using Tyk Operator, ArgoCD, and Kustomize. By following the guide, you'll learn how to manage deployments efficiently in an organization using GitOps principles.
  
## Repository Structure
The repository is organized into three main directories:

```
tyk-operator-demo/
├── apps/
│   └── httpbin/
│       ├── base/
│       └── overlays/
│           ├── prod/
│           └── staging/
├── policies/
│   ├── prod/
│   └── staging/
└── argocd/
    ├── prod/
    └── staging/
```

### 1. `apps/` Directory
Contains Kubernetes manifests for deploying applications. In this example, we're focusing on the `httpbin` application.

- `apps/httpbin/base/`: Base configuration common to all environments.
- `apps/httpbin/overlays/prod/`: Production-specific customizations.
- `apps/httpbin/overlays/staging/`: Staging-specific customizations.

### 2. `policies/` Directory
Stores security policy manifests, governing security options and access rights.

- `policies/prod/`: Security policies for the production environment.
- `policies/staging/`: Security policies for the staging environment.

### 3. `argocd/` Directory
Contains ArgoCD application manifests that automate the deployment process.

- `argocd/prod/`: ArgoCD applications for the production environment.
- `argocd/staging/`: ArgoCD applications for the staging environment.

## Getting started

### Prerequisites

- Familiarity with Kubernetes and Kustomize.
- Basic understanding of Git.
- Access to two Kubernetes clusters (e.g., using Minikube).

### Steps

1. **Fork and Clone the Repository**
    
    Fork this repository to your own GitHub account and then clone it locally:
    
    ```bash
    git clone https://github.com/your-username/tyk-operator-demo.git
    
    cd tyk-operator-demo
    ```
    
2. **Set Up the Environment**
    
    Follow the instructions in the [blog post](#) to set up your staging and production environments using Minikube, Tyk Stack, and ArgoCD.
    
3. **Update ArgoCD Applications**
    
    Modify the `repoURL` in the ArgoCD application manifests under the `argocd/` directory to point to your forked repository.
    
    For example, in `argocd/staging/httpbin.yaml`:
    
    ```yaml
    spec:
      source:
        repoURL: 'https://github.com/your-username/tyk-operator-demo'
    ```
    
4. **Deploy with ArgoCD**
    
    Apply the ArgoCD application manifests to your clusters to deploy the applications and policies.
    
    **For Staging:**
    
    ```
    kubectl config use-context staging
    
    kubectl apply -f argocd/staging-apps.yaml
    ```
    
    **For Production:**
    
    ```
    kubectl config use-context production
    
    kubectl apply -f argocd/prod-apps.yaml
    ```
    
5. **Experiment with Changes**
    
    Modify the `ApiDefinition` or `SecurityPolicy` manifests in the `apps/` or `policies/` directories, then commit and push the changes to your repository.
    
    ```bash
    git add . 
    git commit -m "Your commit message" 
    git push origin main
    ```
    
    ArgoCD will automatically detect and synchronize the changes from Git to Kubernetes. Tyk Operator automatically detect changes of the custom resources and update the live configurations in Tyk accordingly.

## What You've Accomplished
By following this guide and using this repository, you've:

- Set up a comprehensive GitOps workflow.
- Automated deployment of applications and API configurations across multiple environments.
- Utilized Tyk Operator to manage API definitions and security policies as Kubernetes resources.
- Employed ArgoCD for continuous deployment and observed live updates.
- Leveraged Kustomize for environment-specific configurations without duplicating code.
- Gained insights into organizing repositories for scalability and maintainability.

This setup enables efficient management of deployments in an organization, ensuring consistency, reducing manual errors, and accelerating the development workflow.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request if you have suggestions for improvements.

## License

[Mozilla Public License Version 2.0](./LICENSE)

## Questions
For questions on products, please use [Tyk Community forum](https://community.tyk.io/).
  <br>
Clients can also use support@tyk.io.
   <br>
Prospects and evaluators, please use info@tyk.io.
