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

# You can watch the status by running
$ kubectl --namespace ingress-nginx get services -o wide -w ingress-nginx-controller

# Check status of all resources in ingress-nginx namespace:
$ kubectl get all -n ingress-nginx

# Checking runningPods in the namespace.
$ kubectl get pods -n ingress-nginx

# check logs
$ kubectl -n ingress-nginx  logs deploy/ingress-nginx-controller
$ kubectl -n ingress-nginx  logs deploy/ingress-nginx-controller -f # stream

# current deploy
$ kubectl -n ingress-nginx  get deploy

# upgrade helm chart
$ helm upgrade -n ingress-nginx ingress-nginx -f values.yaml .

# Use the following command to see that IP address or FQDN:
$ kubectl get service ingress-nginx-controller --namespace=ingress-nginx
```

## Install test demo app

```bash
$ kubectl create namespace demo

$ kubectl apply -f demo-app.yml -n demo
```

Create Ubuntu app to test connection

```bash
cat <<EOF | kubectl -n demo apply -f -
apiVersion: v1
kind: Pod
metadata:
  name: ubuntu
  labels:
    app: ubuntu
spec:
  containers:
  - name: ubuntu
    image: ubuntu:latest
    command: ["/bin/sleep", "3650d"]
    imagePullPolicy: IfNotPresent
  restartPolicy: Always
EOF


$ kubectl -n demo exec -ti ubuntu -- bash
root@ubuntu:/# apt update && apt install curl -y
root@ubuntu:/# curl apple-service:5678
apple
root@ubuntu:/# curl banana-service:5678
banana
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

# Delete all resources in demo namespace
$ kubectl delete all --all -n demo
$ kubectl delete namespace
```



# References

1. https://platform9.com/learn/v1.0/tutorials/nginix-controller-helm
2. https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/
3. https://computingforgeeks.com/deploy-nginx-ingress-controller-on-kubernetes-using-helm-chart/