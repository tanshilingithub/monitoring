kubectl label nodes 192.168.186.148 rootcloud.com/test=test

kubectl label nodes 172.18.4.90 monitoring=monitoring

192.168.186.148   Ready    control-plane   15m   v1.24.1   
beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=192.168.186.148,kubernetes.io/os=linux,node-role.kubernetes.io/control-plane=,node.kubernetes.io/exclude-from-external-load-balancers=,rootcloud.com/test=test