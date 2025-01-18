
minikube: https://minikube.sigs.k8s.io/docs/start/
kubectl: https://kubernetes.io/docs/tasks/tools/

```
minikube start --nodes=2

minikube stop
minikube start

minikube dashboard
minikube status
```

get info
```
kubectl get pods
kubectl get pods -A

kubectl get svc

kubectl get deployments
kubectl get deployments --all-namespaces

kubectl get jobs
```

apply folder
```
kubectl apply -f k8s

kubectl apply -f k8s/rabbit.yml
```

```
kubectl logs broker-service-96b9c8548-46ct5
```

delete running k8s
```
kubectl delete deployments broker-service mongo rabbitmq

kubectl delete svc broker-service mongo rabbitmq
```

```
# list deployments
kubectl get deployments --all-namespaces

# Where NAMESPACE is the namespace it's in, and DEPLOYMENT is the name of the deployment
kubectl delete -n NAMESPACE deployment DEPLOYMENT
```

run postgres local and connect to k8s
```
docker compose -f postgres.yml up -d
```

stop broker from k8s & expose to outside network
```
kubectl delete svc broker-service
kubectl expose deployment broker-service --type=LoadBalancer --port=8080 --target-port=8080

minikube tunnel
```

stop broker from k8s & re-apply
```
kubectl delete svc broker-service
kubectl apply -f k8s/broker.yml
```

```
minikube addons enable ingress
```

```
kubectl apply -f ingress.yml
kubectl get ingress
```

https://devopscube.com/configure-ingress-tls-kubernetes/


```
kubectl config get-context
```