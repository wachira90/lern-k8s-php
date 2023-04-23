# lern-k8s-php
lerning kubernet php

## create doc root

example current user => user1

```bash
sudo mkdir /var/website
sudo echo "test php" > /var/website/index.html
kubectl create configmap nginx --from-file=/var/website/nginx.conf
sudo echo "<?php phpinfo();?>" > /var/website/index.php
sudo chmod -R 0775 /var/website && sudo chown -R user1:root /var/website
```
