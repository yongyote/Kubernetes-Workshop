# Kubernetes Object
## Configmap and Secret
### Manage Configmap
* kubectl apply configmap logger --from-literal=log_level=debug
* kubectl get configmaps
* kubectl get configmap/logger -o yaml
* kubectl edit configmap/logger
* Change YAML to Read log_level

```
    valueFrom:
        configMapKeyRef:
            name: logger #Read from a configmap called log-level
            key: log_level  #Read the key called log_level
```

### Manage Secret
* kubectl apply secret generic apikey --from-literal=api_key=123456789
* kubectl get secret apikey -o yaml
* kubectl apply -f secretreader-deployment.yaml

```
    valueFrom:
        secretKeyRef:
            name: apikey
            key: api_key
```

## Job and CronJob
* kubectl apply -f simplejob.yaml
* kubectl get jobs
* kubectl get pods --all-pods
* kubectl apply -f cronjob.yaml
* kubectl get cronjobs

## DaemonSet and StatefulSet
* kubectl apply -f daemonset.yaml
* kubectl apply -f daemonset-infra-development.yaml
* kubectl apply -f daemonset-infra-prod.yaml

## Service Proxy with Ingress
What's ingress?
https://kubernetes.io/docs/concepts/services-networking/ingress/

First, we need to add Contour to our cluster.
https://github.com/heptio/contour#add-contour-to-your-cluster

and install Contour with:

* kubectl apply -f https://projectcontour.io/quickstart/contour.yaml
* kubectl apply -f wishlist-contour.yaml
* kubectl get ing
* Consume service from http://localhost/products