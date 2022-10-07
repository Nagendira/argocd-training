So far in all the previous challenges, you have been creating applications via the ArgoCD UI or CLI. An ArgoCD application is essentially a combination of a git repository, an Argo project, several sync options and other values.

This information doesn't need to be confined in Argo CD itself. It can be modeled in a Kubernetes resource so that it can be stored in Git and managed with GitOps as well.

Take a look at https://github.com/codefresh-contrib/gitops-certification-examples/blob/main/declarative/single-app/my-application.yml for an example application

Since our ArgoCD application is now a Kubernetes resource we can handle it like any other kubernetes resource.

We have checked out for you locally the file my-application.yml Apply it with

kubectl apply -f my-application.yml
We have also installed Argo CD for you and you see it in the UI tab.

You should now see the application already in the ArgoCD UI.
