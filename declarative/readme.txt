So far in all the previous challenges, you have been creating applications via the ArgoCD UI or CLI. An ArgoCD application is essentially a combination of a git repository, an Argo project, several sync options and other values.

This information doesn't need to be confined in Argo CD itself. It can be modeled in a Kubernetes resource so that it can be stored in Git and managed with GitOps as well.
