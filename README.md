# capten-templates
Repo to manage Capten Stack Templates.

# capten-templates

* [apps/](./capten-templates/apps)
* [argocd/](./capten-templates/argocd)
  * [apps/](./capten-templates/argocd/apps) --> sub apps folder which are managed by the main app
    * [clusters/](./capten-templates/argocd/apps/clusters)
      * [charts/](./capten-templates/argocd/apps/clusters/charts)
      * [templates/](./capten-templates/argocd/apps/clusters/templates)
        * [cluster-configs/](./capten-templates/argocd/apps/clusters/templates/cluster-configs)
        * [dev/](./capten-templates/argocd/apps/clusters/templates/dev)
        * [prod/](./capten-templates/argocd/apps/clusters/templates/prod)
      * [Chart.yaml](./capten-templates/argocd/apps/clusters/Chart.yaml)
      * [values.yaml](./capten-templates/argocd/apps/clusters/values.yaml)
    * [crossplane/](./capten-templates/argocd/apps/crossplane)
      * [charts/](./capten-templates/argocd/apps/crossplane/charts)
      * [templates/](./capten-templates/argocd/apps/crossplane/templates)
        * [provider-configs/](./capten-templates/argocd/apps/crossplane/templates/provider-configs) 
      * [.helmignore](./capten-templates/argocd/apps/crossplane/.helmignore)
      * [Chart.yaml](./capten-templates/argocd/apps/crossplane/Chart.yaml)
      * [values.yaml](./capten-templates/argocd/apps/crossplane/values.yaml)
    * [tekton/](./capten-templates/argocd/apps/tekton)
      * [charts/](./capten-templates/argocd/apps/tekton/charts)
      * [templates/](./capten-templates/argocd/apps/tekton/templates)
        * [configs/](./capten-templates/argocd/apps/tekton/templates/configs)
        * [pipelines/](./capten-templates/argocd/apps/tekton/templates/pipelines)
      * [Chart.yaml](./capten-templates/argocd/apps/tekton/Chart.yaml)
      * [values.yaml](./capten-templates/argocd/apps/tekton/values.yaml)
  * [main-apps/](./capten-templates/argocd/main-apps) --> This is the main apps folder which needs to be managed manually
    * [clusters-main-app.yaml](./capten-templates/argocd/main-apps/clusters-main-app.yaml) --> polls apps/clusters  folder
    * [crossplane-main-app.yaml](./capten-templates/argocd/main-apps/crossplane-main-app.yaml) --> polls apps/crossplane folder
    * [tekton-main-app.yaml](./capten-templates/argocd/main-apps/tekton-main-app.yaml) --> polls apps/tekton folder
* [cicd/](./capten-templates/cicd)
  * [tekton/](./capten-templates/cicd/tekton)
    * [tekton-pipelines/](./capten-templates/cicd/tekton/tekton-pipelines)
      * [terraform/](./capten-templates/cicd/tekton/tekton-pipelines/terraform)
        * [pipeline.yaml](./capten-templates/cicd/tekton/tekton-pipelines/terraform/pipeline.yaml)
        * [pipelinerun.yaml](./capten-templates/cicd/tekton/tekton-pipelines/terraform/pipelinerun.yaml)
        * [task.yaml](./capten-templates/cicd/tekton/tekton-pipelines/terraform/task.yaml)
    * [tekton-source/](./capten-templates/cicd/tekton/tekton-source)
      * [chart.yaml](./capten-templates/cicd/tekton/tekton-source/chart.yaml)
* [infra/](./capten-templates/infra)
  * [crossplane/](./capten-templates/infra/crossplane)
    * [clusters/](./capten-templates/infra/crossplane/clusters) --> Folder for creating/managing all the clusters
      * [dev/](./capten-templates/infra/crossplane/clusters/dev) --> Cluster specific folder for managing individual clusters
        * [default-apps] --> for managing default apps
        * [apps] --> for managing customer apps
        * [cluster-manifests] --> For managing cluster related yamls
      * [prod/](./capten-templates/infra/crossplane/clusters/prod)
    * [crossplane-config/](./capten-templates/infra/crossplane/crossplane-config)
      * [provider.yaml](./capten-templates/infra/crossplane/crossplane-config/provider.yaml)
      * [providerconfig.yaml](./capten-templates/infra/crossplane/crossplane-config/providerconfig.yaml)
    * [packages/](./capten-templates/infra/crossplane/packages)
      * [k8s/](./capten-templates/infra/crossplane/packages/k8s)
        * [definition.yaml](./capten-templates/infra/crossplane/packages/k8s/definition.yaml)
        * [eks.yaml](./capten-templates/infra/crossplane/packages/k8s/eks.yaml)
    * [providers/](./capten-templates/infra/crossplane/providers)
      * [chart.yaml](./capten-templates/infra/crossplane/providers/chart.yaml)
    * [README.md](./capten-templates/infra/crossplane/README.md)
* [README.md](./capten-templates/README.md)
