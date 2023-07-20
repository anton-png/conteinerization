# Kubernetes network.

## Deployment

### Add the namespace.
```bash
kubectl apply -f namespace.yaml
```

### Deploy PostgreSQL.
```bash
kubectl apply -f pgsql/pv.yaml && \
kubectl apply -f pgsql/pvc.yaml && \
kubectl apply -f pgsql/secret.yaml && \
kubectl apply -f pgsql/configmap.yaml && \
kubectl apply -f pgsql/deployment.yaml && \
kubectl apply -f pgsql/service.yaml
```

### Deploy Redmine.
```bash
kubectl apply -f redmine/secret.yaml && \
kubectl apply -f redmine/configmap.yaml && \
kubectl apply -f redmine/deployment.yaml && \
kubectl apply -f redmine/service.yaml
```

### Add the Ingress.
```bash
kubectl apply -f ingress.yaml
```

## Result of checking.

![alt text](https://github.com/anton-png/conteinerization/blob/main/assets/IMG_03.png?raw=true)

