# lern-k8s-php
lerning kubernet php

## quick start

linux current user => user1

```bash
cd /var
sudo git clone https://github.com/wachira90/lern-k8s-php.git
sudo mv lern-k8s-php/ website/
sudo chmod -R 0775 /var/website && sudo chown -R user1:root /var/website
cd website/
kubectl apply -f . -n test
```

## delete

```bash
kubectl delete -f . -n test
```

## test

```
http://localhost:30000
```

## option when add domain

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
