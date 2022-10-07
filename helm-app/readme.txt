Using ArgoCD CLI
Step 1
Apart from the UI, ArgoCD also has a CLI. We have installed already the cli for you and authenticated against the instance.

Try the following commands

argocd app list
argocd app get helm-gitops-example
argocd app history helm-gitops-example
Let's delete the application and deploy it again but from the CLI this time.

First delete the app

argocd app delete helm-gitops-example
Confirm the deletion by answering yes in the terminal. The application will disappear from the Argo CD dashboard after some minutes.

Now deploy it again.

argocd app create demo \
--project default \
--repo https://github.com/codefresh-contrib/gitops-certification-examples \
--path "./helm-app/" \
--sync-policy auto \
--dest-namespace default \
--dest-server https://kubernetes.default.svc
The application will appear again in the ArgoCD dashboard.

Confirm the deployment

kubectl get all
Finish
If you've confirmed the deployment, click Check to finish this track.

