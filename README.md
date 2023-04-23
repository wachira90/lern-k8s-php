# lern-k8s-php
lerning kubernet php

## quick start

example current user => user1

```bash
cd /var/
git clone https://github.com/wachira90/lern-k8s-php
mv lern-k8s-php/ website/
sudo chmod -R 0775 /var/website && sudo chown -R user1:root /var/website
kubectl create configmap nginx --from-file=/var/website/nginx.conf
kubectl apply -f .
```
