So far in all the previous challenges, you have been creating applications via the ArgoCD UI or CLI. An ArgoCD application is essentially a combination of a git repository, an Argo project, several sync options and other values.

This information doesn't need to be confined in Argo CD itself. It can be modeled in a Kubernetes resource so that it can be stored in Git and managed with GitOps as well.

Take a look at https://github.com/codefresh-contrib/gitops-certification-examples/blob/main/declarative/single-app/my-application.yml for an example application

Since our ArgoCD application is now a Kubernetes resource we can handle it like any other kubernetes resource.

We have checked out for you locally the file my-application.yml Apply it with

kubectl apply -f my-application.yml
We have also installed Argo CD for you and you see it in the UI tab.

You should now see the application already in the ArgoCD UI.

Use App of Apps
-------------------------------------------------------------------------------------------------------
We can delete the application like any other Kubernetes resource

kubectl delete -f my-application.yml
After a while the application should disappear from the ArgoCD UI.

Remember however that the whole point of GitOps is to avoid manual kubectl commands. We want to store this application manifest in Git. And if we store it in Git, we can handle it like another GitOps application!

ArgoCD can manage any kind of Kubernetes resources and this includes its own applications (inception).

So we can commit multiple applications in Git and pass them to ArgoCD like any other kind of manifest. This means that we can handle multiple applications as a single one.

We already have such example at https://github.com/codefresh-contrib/gitops-certification-examples/tree/main/declarative/multiple-apps.

In the ArgoCD UI, click the "New app" button on the top left and fill the following details:

application name : 3-apps
project: default
SYNC POLICY: automatic
repository URL: https://github.com/codefresh-contrib/gitops-certification-examples
path: ./declarative/multiple-apps
Cluster: https://kubernetes.default.svc (this is the same cluster where ArgoCD is installed)
Namespace: argocd
Notice that the namespace value is the namespace where the parent Application is deployed and not the namespace where the individual applications are deployed. ArgoCD applications must be deployed in the same namespace as ArgoCD itself.

Leave all the other values empty or with default selections. Finally click the Create button.

ArgoCD will deploy the parent application and its 3 children. Click on the parent application. You should see the following.three-apps

Spend some time on the UI to understand where each application is deployed. You can also use the command line

kubectl get all -n demo1
kubectl get all -n demo2
kubectl get all -n demo3
