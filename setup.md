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

#Start minikube
start it 
- minikube start --driver=docker --cpus=4 --memory=8g

set kubectl context to minikube
- kubectl config use-context minikube

