Install the Argo Rollouts controller
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

Wait some time until the controller is fully synced and the deployment is marked as Healthy.

Once you are ready to proceed, press Check.



Install Ambassador
Blue/Green deployments can work on any vanilla Kubernetes cluster. But for Canary deployments you need a smart service layer that can gradually shift traffic to the canary pods while still keeping the rest of the traffic to the old/stable pods.

Argo Rollouts supports several service meshes and gateways for this purpose.

In this lesson we will use the popular Ambassador API Gateway for Kubernetes to split live traffic between the canary and old/stable version.

We installed Argo CD for you and you can login in the UI tab.

Click the "New app" button on the top left and fill the following details:

application name : ambassador
project: default
SYNC POLICY: automatic
AUTO-CREATE Namespace: enabled
repository URL: https://github.com/codefresh-contrib/gitops-certification-examples
path: ./ambassador-chart
Cluster: https://kubernetes.default.svc (this is the same cluster where ArgoCD is installed)
Namespace: ambassador
Leave all the other values empty or with default selections. Finally click the Create button. The Ambassador Gateway will be installed on the cluster.

Notice that we are not using the default namespace, but a brand new one. It is imperative that you select the "auto-create namespace" option.

auto-create

If you don't select this option, ArgoCD will not find the namespace and deployment will fail. Delete the application and create it again if you have a deployment issue.

You can also manually do if you forgot it in the UI:

kubectl create namespace ambassador
Try syncing again the application.

Again, you can see that GitOps is not only useful for your own applications but also for other supporting applications as well.






The first deployment
The Argo Rollouts controller is running now on the cluster and it is ready to handle deployments.

Lets deploy our application. Since this is the first deployment, there is no previous version and thus a normal deployment will take place.

We installed Argo CD for you and you can login in the UI tab.

Click the "New app" button on the top left and fill the following details

application name : demo
project: default
SYNC POLICY: Manual
repository URL: https://github.com/codefresh-contrib/gitops-certification-examples
path: ./canary-app
Cluster: https://kubernetes.default.svc (this is the same cluster where ArgoCD is installed)
Namespace: default
Leave all the other values empty or with default selections.

Finally click the Create button. The application entry will appear in the main dashboard. Click on it.

The application will be initially "Out of Sync". Press the sync button to sync it and wait until it is healthy.

The application is deployed and you can see it in the "Live traffic" tab. You should see the following.

version1

Argo Rollouts also has an optional CLI that can be used for monitoring and promoting deployments

We have already installed kubectl argo rollouts for you in this exercise. And we can use it to monitor the first deployment

Run the following

kubectl argo rollouts list rollouts
kubectl argo rollouts status simple-rollout
kubectl argo rollouts get rollout simple-rollout
The last command shows the status of the rollout. Since this is the first version there is only one replicaset with ten pods.

You can also see this with

kubectl get rs
