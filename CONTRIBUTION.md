# Contribution Guidelines:
Please read this guide if you plan to contribute to this repo. We welcome any kind of contribution.

## Reporting Issues:
If you find a bug while working with capten-templates, please [open an issue on GitHub](https://github.com/intelops/capten-templates/issues/new?labels=kind%2Fbug&template=bug-report.md&title=Bug:) and let us know what went wrong. We will try to fix it as quickly as we can.

## Feature Requests:
You are more than welcome to open issues in this project to [suggest new features](https://github.com/intelops/capten-templates/issues/new?labels=kind%2Ffeature&template=feature-request.md&title=Feature%20Request:).

## Directory Structure

```
capten-templates/
│
├── cicd/
│   ├── tekton-cluster-tasks			# Custom tekton tasks.
│   │   └── templates/
│   ├── tekton-pipelines			# Pipelines are synced via argocd.
│   │   └── templates/
│   └── tekton
│       ├── argocd-apps/			# Argocd apps related to tekton directory.
│       │   └── templates/
│       ├── pipeline-template/		# Tekton pipelines are stored in template format.
│       │   └── templates/
│       └── tekton-main-app.yaml		# Argocd main app for tekton directory.
│
├── default-apps-templates/			# Default apps for the cluster.
│   ├── values
│   └── app_list.yaml
│
├── infra/
│   ├── clusters
│   │   ├── app-configs/			# All apps related to the cluster (synced via argocd).
│   │   ├── argocd-apps/			# Argocd apps related to clusters directory.
│   │   │   └── templates/
│   │   │       ├── cluster-apps/
│   │   │       └── cluster-compositions/
│   │   ├── cluster-configs/			# Cluster claim yaml file.
│   │   ├── compositions/			# Composition yaml file.
│   │   │   └── aws/
│   │   └── clusters-main-app.yaml		# Argocd main app for clusters directory.
│   └── crossplane
│       ├── argocd-apps/			# Argocd apps related to crossplane directory.
│       │   └── templates/
│       │       ├── package-k8s/
│       │       │   └── aws-packages/
│       │       └── providers/
│       ├── packages-def/			# Provider config and composite resource definition.
│       │   └── k8s/
│       │       └── aws/
│       ├── providers				# Providers are deployed here once synced via capten.
│       └── crossplane-main-app.yaml		# Argocd main app for crossplane directory.
│
├── tekton-samples/				# Examples related to external secrets and tekton components.
│   ├── external-secrets/
│   │   ├── github-external-secrets/
│   │   └── gitlab-external-secrets/
│   └── tekton-pipeline-yamls/
```

## How to contribute to capten-templates:
You can generally contribute capten-templates in 4 ways:

1. Updating and adding new providers
2. Adding new addons and components in crossplane composition as required
3. Applying crossplane files depending on the cloud providers deployed
4. Adding custom tasks
5. Adding new registry as a source for tekton

### 1. Updating and adding new providers:
As mentioned above, the providers are present in the directory infra/crossplane/providers. You can add new providers in this directory.
Also, new packages will constantly be updated by crossplane for different cloud providers. They can be updated in the package section in the provider yaml file.

```
apiVersion: pkg.crossplane.io/v1
kind: Provider
metadata:
  name: provider-aws
spec:
  package: xpkg.upbound.io/crossplane-contrib/provider-aws:v0.33.0
```

### 2. Adding new addons and components in crossplane composition as required
Addons and components can be appended in crossplane composition file. The composition file is present under infra/clusters/compositions/aws/eks.yaml
New components and addons can be added under the resources section under a new name. An example using vpc is shown below:
(Please refer crossplane documents on how to initialize patches using both the definition and composition file).

```
- name: vpc-nodepool
    base:
      apiVersion: ec2.aws.crossplane.io/v1beta1
      kind: VPC
      spec:
        forProvider:
          region: us-west-2
          cidrBlock: 10.0.0.0/16
          enableDnsSupport: true
    patches:
    - fromFieldPath: spec.id
      toFieldPath: metadata.name
```

### 3. Applying crossplane files depending on the cloud providers deployed:
Presently, we are supporting aws cloud provider. As more cloud providers come into the picture, we need to deploy the yaml files specific to the cloud provider deployed. Any contributions regarding this aspect is welcome.

### 4. Adding custom tasks:
Custom tasks are stored under the directory cicd/tekton-cluster-tasks. Any new custom tasks can be added here.

### 5. Adding new registry as a source for tekton:
At present we have external secrets for github and gitlab registries under the directory tekton-samples/external-secrets. External secrets with new registries can be added here.


## Directory rundown:
Let us have a brief look at all the 4 main directories in capten-templates one by one.

1. cicd
2. default-apps-templates
3. infra
4. tekton-samples

**Note:** Argocd apps sub-directory in each directory will manage deployment of the same directory which is watched by a main app.

1. cicd:
  - tekton-cluster-tasks -> Custom tekton tasks are given here. You can add new ones as required
  - tekton-pipelines -> Empty by default. Will be deployed via argocd.
  - tekton/pipeline-template -> Pipelines are stored as templates.
  
2. default-apps-templates:
  - values -> helm values of default apps are stored here.
  - app_list.yaml -> list of helm charts of all default apps.
  
3. infra:
  - clusters/app-configs -> Empty by default. Will be deployed via argocd once cluster is created.
  - clusters/cluster-configs -> Empty by default. User is required to add cluster-claim yaml to trigger cluster creation.
  - clusters/compositions -> Composition file is stored here.
  
  - crossplane/packages-def -> Provider config and composite resource definition are stored here.
  - crossplane/providers -> Empty by default. Will be deployed once capten is synced.
  
4. tekton-samples:
  - Example formats related to external secrets and tekton yaml files
