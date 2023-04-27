# lern-k8s-php
lerning kubernet php

## Quick start

```
php:fpm-alpine
php:7.4.33-fpm-alpine3.16
php:7.3.33-fpm-alpine3.15
php:7.2.34-fpm-alpine3.12
php:7.1.33-fpm-alpine3.10
php:7.0.33-fpm-alpine3.7
```

Linux current user => user1

```bash
cd /mnt
sudo git clone https://github.com/wachira90/lern-k8s-php.git
sudo chmod -R 0775 /mnt/lern-k8s-php && sudo chown -R user1:root /mnt/lern-k8s-php
cd lern-k8s-php/
kubectl apply -f . -n test
```

## Delete

```bash
kubectl delete -f . -n test
```

## Test

```
http://localhost:30000
```

## Option when add domain

```yml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: test-ingress
  namespace: test
  annotations:
    nginx.ingress.kubernetes.io/ssl-redirect: "false"  
  labels:
    app: nginx
    layer: frontend
spec:
  ingressClassName: public
  rules:
  - host: kube-server.inno.test
    http:
      paths:
        - pathType: Exact
          path: "/"
          backend:
            service:
              name: nginx
              port:
                number: 80
---
apiVersion: v1
kind: Service
metadata:
  name: nginx
  namespace: test
  labels:
    app: nginx
    layer: frontend
spec:
  type: ClusterIP
  selector:
    app: nginx
  ports:
  - port: 80
    protocol: TCP
```
