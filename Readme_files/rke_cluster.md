## create three ubuntu machines.
### on the three nodes(Rancher-UI-Node1,Rancher-UI-Node2,Rancher-UI-Node-3), run below commands
```
#!/bin/bash
curl https://get.docker.com/ | bash
usermod -a -G root ubuntu
usermod -a -G docker ubuntu
sudo systemctl daemon-reload
sudo systemctl restart docker
```

- In the [rke-cluster.yml](YML/rke-cluster.yml) , provide pem file path and the ipaddresses of the nodes.
If it is AWS, provide public IPs.
- Download the rke from releases of [rke](https://github.com/rancher/rke) repo and set to PATH on your system.
  ```
  #By cd to the file where the cluster yml file is there.
  rke version
  rke up help
  rke up --config rke-clutser.yml  ##it will generate a kube config file also after deploying the cluster.
  ```
