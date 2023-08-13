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
- Install kubectl and use this config to test the cluster.

## Steps to install Rancher UI
- go to this [link](https://ranchermanager.docs.rancher.com/v2.0-v2.4/pages-for-subheaders/install-upgrade-on-a-kubernetes-cluster) and use 6. Install Rancher with Helm and Your Chosen Certificate Option with Let's encrypt tab selected.
```
kubectl create namespace cattle-system  ## step 3
helm repo add rancher-latest https://releases.rancher.com/server-charts/latest  ##step 2
helm repo update

##step 5

# Create the namespace for cert-manager
kubectl create namespace cert-manager

# Add the Jetstack Helm repository
helm repo add jetstack https://charts.jetstack.io

# Update your local Helm chart repository cache
helm repo update

# Install the cert-manager Helm chart
helm install \
  cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --version v1.0.4
##step 6  replace rancher.my.org with your domain
helm install rancher rancher-latest/rancher \
  --namespace cattle-system \
  --set hostname=rancher.my.org \
  --set bootstrapPassword=randomepasswordgenerated \
  --set ingress.tls.source=letsEncrypt \
  --set letsEncrypt.email=me@example.org    
```
