



install kubeshpere on k8s
为了使用本地配置的情况
```shell
kubectl apply -f /local_file/kubesphere/kubesphere-installer.yaml
kubectl apply -f /local_file/kubesphere/cluster-configuration.yaml
kubectl apply -f /local_file/kubesphere/bundle.yaml
```


debug
```shell
kubectl logs -n kubesphere-system $(kubectl get pod -n kubesphere-system -l 'app in (ks-install, ks-installer)' -o jsonpath='{.items[0].metadata.name}') -f
kubectl -n kubesphere-system get pod|grep ks-installer|awk '{print $1}' | xargs kubectl -n kubesphere-system delete pod
kubectl -n kubesphere-system get pod
kubectl -n kubesphere-system describe pod ks-installer-746f68548d-gn24s
kubectl get pvc -A
kubectl -n kubesphere-system get configmap
kubectl get pod -A|grep -v Running

kubectl -n kubesphere-system describe pod ks-apiserver-567fcb899d-4r9s5
kubectl -n kubesphere-system describe pod ks-controller-manager-5d8b59b66f-d7wt5
kubectl -n kubesphere-system logs -f --tail 300 deploy/ks-apiserver

kubectl -n kubesphere-system delete pod ks-apiserver-567fcb899d-4r9s5
kubectl -n kubesphere-system delete pod ks-controller-manager-5d8b59b66f-d7wt5
```

login
```shell
http://IP:30880   admin/P@88w0rd

```
