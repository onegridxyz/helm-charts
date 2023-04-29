# helm-charts

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
