#Install minikube
Note on environment
- This is on WSL, where docker desktop is installed on Windows...
- We'll install and run Minikube inside WSL, using the --driver=docker option.

curl latest version of minikube binary (from official source?) ...
- curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
- note: don't use app package manager (apt-get) because minikube team doesn't maintain an offical APT repository

Install minikube
- sudo install minikube-linux-amd64 /usr/local/bin/minikube

Install kubectl
- because minikube doesn't include per se (you can run "minikube kubectl...", but that is less convenient syntax...and also only works for minikube...its not the kubectl that we'd use with other clusters launchers...)
- curl -LO "https://dl.k8s.io/release/$(curl -sL https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
- chmod +x kubectl
- sudo mv kubectl /usr/local/bin/

Confirm kubectl is installed and path picks it up right
- which kubectl
  - should return /usr/local/bin/kubectl

#Install helm
- curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
  - this script installs helm into /usr/local/bin
#Start minikube
start it 
- minikube start --driver=docker --cpus=4 --memory=2200mb
  - note: if have more resources, could increase memory(?)

set kubectl context to minikube
- kubectl config use-context minikube
- btw, helm knows what kubernetes cluster to work on based on this
- btw....context is defined in the file ~/.kube/config (use-context sets this(?)

#Helm repo, etc. type prep
Add promethius-community repo to local helm
- helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
Update helm repos installed
- helm repo update

#Install prom-stack
- helm install kube-prom-stack prometheus-community/kube-prometheus-stack
- Note: Prom-stack includes
  - Prometheus (metrics collection)
  - Alertmanager (to send alerts based on Prometheus rules)
  - Grafana (for dashboards and visualizations)
  - node-exporter (exports node-level metrics)
  - kube-state-metrics (exports Kubernetes object states)
  - Custom dashboards and alert rules
- Note: helm install doesn't add a helm chart yaml to file system...it does everything on the fly...:
  - gets the templates/renders the templates(?)
  - sends resulting Kubernetes YAML manifests directly Kubernetes API servers (then Kubernetes then creates the resources)
- Aside: Just for learning, also do the following to get an output of the helm chart...view it...understand better what prom-stack is/has configured
  - helm template kube-prom-stack prometheus-community/kube-prometheus-stack > prometheus-stack-not-used-just-for-viewing.yaml
- review install messages (tells you how to access alert manager, grafana, etc)
  - helm get notes kube-prom-stack