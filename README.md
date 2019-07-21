# k8s-test
Testing k8s deployments

# This is tested with Kubernetes in Docker For Desktop

You have to install nginx-ingress-controller

https://github.com/kubernetes/ingress-nginx/blob/master/docs/deploy/index.md

```console
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/mandatory.yaml
```

```console
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/cloud-generic.yaml
```

# Create deployments, services and ingress

```console
kubectl apply -f api-deployment.yml
kubectl apply -f api-service.yml
kubectl apply -f api-ingress.yml
```

```console
kubectl apply -f ui-deployment.yml
kubectl apply -f ui-service.yml
kubectl apply -f ui-ingress.yml
```

# Access de swagger-ui

http://localhost/ui/

The UI is also accessing the api endpoint at:

http://localhost/v2/swagger.json

# Stop the environment

```console
kubectl delete deployments,services,ingress --all
```

WARNING: This is going to remove default kubernetes service but the cluster is going to restart

# Testing HPA

Follow instructions here: https://medium.com/@dstrimble/kubernetes-horizontal-pod-autoscaling-for-local-development-d211e52c309c

```console
kubectl apply -f hpa-deployment.yml
```

Now you can run a loadtest with taurus docker image

```console
kubectl run -i --tty load-generator --image=blazemeter/taurus -- http://localhpatest.default.svc.cluster.local:8080/
```
