helm install testingefs efsprovisioner/ --dry-run --set efsid="fs-5c15abe8"
helm install testingefs efsprovisioner  --set efsid="fs-5c15abe8"
kubectl get po
kubectl get pv
kubectl get pvc
helm ls
helm uninstall testingefs
