# helm-charts

```bash
# Add helm repository
$ helm repo add nginx-stable https://helm.nginx.com/stable
$ helm repo update
$ helm install onegrid-ingress nginx-stable/nginx-ingress
$ helm show values nginx-stable/nginx-ingress # show values

$ kubectl get pods
$ kubectl get deployments
$ kubectl get services

$ kubectl port-forward service/nginx 8080:80
```
