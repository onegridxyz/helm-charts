# helm-charts

## Install Nginx Ingress Controller

```bash
# Download nginx-controller
$ controller_tag=$(curl -s https://api.github.com/repos/kubernetes/ingress-nginx/releases/latest | grep tag_name | cut -d '"' -f 4)
$ wget https://github.com/kubernetes/ingress-nginx/archive/refs/tags/${controller_tag}.tar.gz

# Extract the file downloaded:
$ tar xvf ${controller_tag}.tar.gz

# Switch to the directory created:
$ cd ingress-nginx-${controller_tag}

# Change your working directory to charts folder:
$ cd charts/ingress-nginx/

# Create namespace
$ kubectl create namespace ingress-nginx
```

## Utilities

```bash
# Add helm repository
$ helm repo add nginx-stable https://helm.nginx.com/stable
$ helm repo update
$ helm install nginx-ingress nginx-stable/nginx-ingress --set rbac.create=true
$ kubectl get pods --all-namespaces -l app=nginx-ingress-nginx-ingress
$ kubectl get services nginx-ingress-nginx-ingress
$ helm show values nginx-stable/nginx-ingress # show values

$ helm install nginx-stable/nginx-ingress --set controller.service.loadBalancerIP=XXXX,rbac.create=true


$ kubectl get pods
$ kubectl get deployments
$ kubectl get services

$ kubectl port-forward service/onegrid-ingress-nginx-ingress-controller 8080:80
```



# References

1. https://platform9.com/learn/v1.0/tutorials/nginix-controller-helm
2. https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/
3. https://computingforgeeks.com/deploy-nginx-ingress-controller-on-kubernetes-using-helm-chart/