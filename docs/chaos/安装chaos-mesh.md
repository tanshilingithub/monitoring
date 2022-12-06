安装(containerd场景)
```shell
helm repo add chaos-mesh https://charts.chaos-mesh.org
kubectl create ns chaos-mesh
helm install chaos-mesh chaos-mesh/chaos-mesh -n=chaos-mesh --set chaosDaemon.runtime=containerd --set chaosDaemon.socketPath=/run/containerd/containerd.sock

```

verify
```shell
kubectl get po -n chaos-mesh -o wide
kubectl -n chaos-mesh describe pod chaos-controller-manager-58cc5d8d58-rr2gg
```