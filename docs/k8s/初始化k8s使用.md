标签设计:
    场景(scenes)、承载物(carrier)
    默认值为all, 同级多个折叠时使用--进行扁平化, 例如flink、flink-jobmanager、eca-flink

```shell
kubectl label nodes 192.168.186.148 rootcloud.com/scenes=test
kubectl label nodes 192.168.186.148 rootcloud.com/carrier=test
#kubectl label nodes 192.168.186.148 rootcloud.com/scenes-
#kubectl label nodes 192.168.186.148 rootcloud.com/carrier-



```



验证
```shell
kubectl get node --show-labels|grep rootcloud.com



192.168.186.148   Ready    control-plane   13h   v1.24.1   
beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64
,kubernetes.io/hostname=192.168.186.148,kubernetes.io/os=linux
,node-role.kubernetes.io/control-plane=,node.kubernetes.io/exclude-from-external-load-balancers=
,rootcloud.com/carrier=all,rootcloud.com/scenes=all
```