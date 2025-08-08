Start minikube cluster after deploying from helm chart (with helm install)
- Context: Deployed to cluster with "helm install...."...then, restarted host machine where cluster lives...don't worry, its stored ...in etcd (kubernetes DB)
- minikube start (starts cluster...had deployments saved)
- kubectl get pods -A ... to confirm they are running
- Note...this is the same for a deployment created using a .yaml file...btw.