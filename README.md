# install-prometheus-and-grafana-on-kubernetes

# Install Prometheus and Grafana using Helm
below are the steps to install prometheus and grafana on a kubernetes cluster using helm

## Requirments
- helm
- kubectl

## step 1: add the helm repository
```sh
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
```
## step 2: update helm repository
```sh
helm repo update
```
## step 3: Create a namespace monitoring 
```sh
kubectl create ns monitoring
```
## step 4: Install prometheus and grafana
```sh
helm install prometheus --namespace monitoring prometheus-community/kube-prometheus-stack
```
## step 5 : Edit the prometheus-grafana service type to LoadBalancer
```sh
kubectl edit svc prometheus-grafana -n monitoring
```
## step 5 : Get the admin user and password  
```sh
kubectl get secret prometheus-grafana -n monitoring -o jsonpath="{.data.admin-user}" | base64 --decode ; echo
kubectl get secret prometheus-grafana -n monitoring -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```

