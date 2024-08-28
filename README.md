# keda
A lab showcasing KEDA (Kubernetes Event Driven Autoscaler), follow along.

# To replicate

1. Spin up a local development kubernetes cluster (I suggest kind)
```
kind create cluster -n keda
```

# Deploying KEDA
```
helm repo add kedacore https://kedacore.github.io/charts
helm repo update
helm upgrade -i keda kedacore/keda --namespace keda --create-namespace
```

```
kubectl create deploy myapp --image nginx --replicas=2

kubectl apply -f cron.yaml

kubectl get scaledobject.keda.sh
```

# You should be able see the no. of pods being increased to upto 10 based on the cron configuration


## Useful Commands
```
alias k='kubectl'
k apply -f webapp.yaml
kubectl port-forward deploy/webapp 8080:80

curl http://localhost:8080/
```

## Use load testing & benchmarking utility siege to simulate scaling requirement:-
```
siege -q -c 2 -t 1m http://localhost:8080
k apply -f hpa.yaml

kubectl get hpa -w
```

Check the no. of pods being increased

## Clean up
```
kubectl delete hpa webapp
kubectl delete deploy webapp
```

That's about it...


## Reference
KEDA Official Website
[Keda-official](
https://keda.sh/)


Deploying KEDA to kubernetes cluster
[deploy-keda](
https://keda.sh/docs/2.12/deploy/)

KEDA Source code can be found at:-
[keda-source-code](
https://github.com/kedacore/keda)