#Install minikube
Note on environment
- This is on WSL, where docker desktop is installed on Windows...
- We'll install and run Minikube inside WSL, using the --driver=docker option.

curl latest version of minikube binary (from official source?) ...
- curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
- note: don't use app package manager (apt-get) because minikube team doesn't maintain an offical APT repository

Install minikube
- sudo install minikube-linux-amd64 /usr/local/bin/minikube

#Start minikube
minikube start --driver=docker --cpus=4 --memory=8g

