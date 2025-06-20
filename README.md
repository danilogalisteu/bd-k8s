
## Installation

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client
```

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
sudo dpkg -i minikube_latest_amd64.deb
minikube start --extra-config "apiserver.cors-allowed-origins=["http://boot.dev"]"
kubectl version
```

## Addons

```bash
# kubectl top
minikube addons enable metrics-server
# ingress
minikube addons enable ingress
```

## Configuration

```bash
kubectl create deployment synergychat-web --image=docker.io/bootdotdev/synergychat-web:latest
kubectl edit deployment synergychat-web
kubectl get deployment synergychat-web -o yaml

kubectl apply -f <config-file>

kubectl delete pod <pod-name>
```

## Status

```bash
kubectl get pod -A
kubectl get pod -o wide
kubectl get pod
kubectl get replicaset
kubectl get configmap
kubectl get deployment
kubectl get service
kubectl get pvc
kubectl get pv
kubectl get hpa

kubectl top pod

kubectl logs <pod-name>
kubectl describe pod <pod-name>
```

## Namespaces

```bash
kubectl create ns <namespace>
kubectl -n <namespace> get pods
kubectl -n <namespace> get svc
kubectl -n <namespace> get configmaps
```

The default namespace is `default`.

Automatic DNS entry for services:
`<service-name>.<namespace>.svc.cluster.local`

## Connections

Single:
`kubectl port-forward <pod-name> 8080:8080`

All:
`kubectl proxy`

With an active ingress (and DNS pointing to it):
`minikube tunnel -c`
