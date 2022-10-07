nstall the Argo Rollouts controller
Before we get started with progressive delivery we need to install the Argo Rollouts controller on the cluster.

We installed Argo CD for you and you can login in the UI tab.

The UI starts empty because nothing is deployed on our cluster. Click the "New app" button on the top left and fill the following details:

application name : argo-rollouts-controller
project: default
SYNC POLICY: automatic
AUTO-CREATE Namespace: enabled
repository URL: https://github.com/codefresh-contrib/gitops-certification-examples
path: ./argo-rollouts-controller
Cluster: https://kubernetes.default.svc (this is the same cluster where ArgoCD is installed)
Namespace: argo-rollouts
Leave all the other values empty or with default selections. Finally click the Create button. The controller will be installed on the cluster.

Notice that we are not using the default namespace, but a brand new one. It is imperative that you select the "auto-create namespace" option.

auto-create

If you don't select this option, ArgoCD will not find the namespace and deployment will fail. Delete the application and create it again if you have a deployment issue.

You can also manually do if you forgot it in the UI:

kubectl create namespace argo-rollouts
Try syncing again the application.

You can see that GitOps is not only useful for your own applications but also for other supporting applications as well.

Wait some time until the controller is fully synced and the deployment is marked as Healthy
