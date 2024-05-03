# Monitoring Kubernetes Cluster with Prometheus
This repository provides step-by-step instructions for configuring Prometheus and Grafana to create a monitoring infrastructure for Kubernetes clusters. Users can create a reliable monitoring system to keep tabs on the condition, functionality, and resource usage of their Kubernetes installations by following the instructions provided below. To ensure smooth scaling and thorough coverage of the Kubernetes cluster, we also incorporate service discovery into Prometheus to automatically identify and incorporate additional nodes into the monitoring system.
## Installation

## Docker Installation

First you have to uninstall old versions. 
bash
$ sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine


Then begin the installation process:

1. Install `` yum-utils`` package:
bash 
$ sudo yum install -y yum-utils 


2. Add docker-ce.repo repository to download Docker:
bash 
$ sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo 

3. Installing Docker packages:
bash 
$ sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin 

4. Enabling Docker service:
bash 
$ sudo systemctl enable --now docker


## Install and Set Up kubectl

1. Download the latest release with the command:
bash 
$ curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl


2. Make the kubectl binary executable:
bash 
$ chmod +x ./kubectl


3. Move the binary into your PATH:
bash 
$ sudo mv ./kubectl /usr/local/bin/kubectl


4. Verifying Installation:
bash 
$ kubectl version


## Minikube Installation

1. Download Minikube last release:
bash 
$ curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

2. Install Minikube package:
bash 
$ sudo install minikube-linux-amd64 /usr/local/bin/minikube

3. Start Minikube:
bash 
$ minikube start --driver=docker --force


<img width="581" alt="Screenshot 2024-05-02 221328" src="https://github.com/eemankhaled/Prometheus-Project/assets/161209853/0bcb42f0-d486-45ff-8c20-601ec1ec869d">



## Helm Installation

1. Fetch that script:
bash 
$ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3

2. Provide execute permission to the file:
bash 
$ chmod 700 get_helm.sh

3. Run the script:
bash 
$ ./get_helm.sh



### Deploy Prometheus
1.Add Prometheus Helm repository
bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

2.Update the Helm repositories:
bash
helm install prometheus prometheus-community/prometheus

3.Install Prometheus using Helm:
bash
helm repo update

4.Expose Prometheus Service:
bash
kubectl expose service prometheus-server — type=NodePort — target-port=9090 — name=prometheus-server-ext

<img width="581" alt="Screenshot 2024-05-02 221328" src="https://github.com/eemankhaled/Prometheus-Project/assets/161209853/b60b47e9-cc60-469c-88dd-a02ca286795f">

5.Open Web App of Prometheus
bash
minikube service prometheus-server-ext




### Deploy Grafana

1.Add Grafana Helm repository:
bash
helm repo add grafana https://grafana.github.io/helm-charts

2.Update the Helm repositories:
bash
helm install grafana grafana/grafana

3.Install Grafana using Helm:
bash
helm repo update

4.Expose Grafana service:
bash
kubectl expose service grafana — type=NodePort — target-port=3000 — name=grafana-ext

5.Open Grafana Web APP
bash
minikube service grafana-ext




### Get Grafana Credintials
bash
kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo


### Conclusion

Ultimately, this project set up and configured important tools including Helm, Prometheus, Grafana, Docker, Kubectl, Minikube, and Minikube to allow efficient Kubernetes environment monitoring. We were able to obtain important insights into our Kubernetes cluster's health, performance, and resource use by employing Prometheus and Grafana to gather, store, and visualize metrics from our cluster. We can keep an eye on things and address problems quickly with this configuration, which guarantees the reliability and dependability of our Kubernetes services.



### Outputs

<img width="644" alt="Screenshot 2024-05-02 221452" src="https://github.com/eemankhaled/Prometheus-Project/assets/161209853/0d6bf31f-94f3-4576-941d-87f15e4ec746">

![photo_2024-05-03_22-03-39](https://github.com/eemankhaled/Prometheus-Project/assets/161209853/ae674c83-5620-4c0c-9597-619cf0c341ad)
