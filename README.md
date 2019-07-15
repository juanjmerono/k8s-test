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

kubectl apply -f api-deployment.yml
kubectl apply -f api-service.yml
kubectl apply -f api-ingress.yml

kubectl apply -f ui-deployment.yml
kubectl apply -f ui-service.yml
kubectl apply -f ui-ingress.yml

# Access de swagger-ui

http://localhost/ui/

The UI is also accessing the api endpoint at:

http://localhost/v2/swagger.json

# Stop the environment

kubectl delete deployments,services,ingress --all

WARNING: This is going to remove default kubernetes service but the cluster is going to restart
