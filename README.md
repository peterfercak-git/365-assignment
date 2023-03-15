# 365.innohub assignment
## Expose NGINX on port 80 (EC2)

## Options
- eksctl CLI tool (simple and straighforward)
- create EC2 instance, pass user data and use Minikube to create a K8s cluster
- Terraform Kubernetes provider
  - https://registry.terraform.io/providers/hashicorp/kubernetes/latest/docs

## Minikube

Create minikube cluster on VM:
```sh
minikube start --kubernetes-version=v1.23.2 --driver=none
```

Create a namespace "my-ns":

```sh
kubectl create ns my-ns
```

Create a deployment for the NGINX image with 1 replica:

```sh
kubectl create deployment my-nginx --image=nginx -n my-ns
```

Make the deployment available on port 80 via kubernetes service of a type NodePort:

```sh
kubectl expose deployment my-nginx --type=NodePort --port=80 -n my-ns
```

## eksctl CLI

Create a simple EKS cluster:

```sh
eksctl create cluster
```

EKS on Fargate:

```sh
eksctl create cluster --fargate
```
