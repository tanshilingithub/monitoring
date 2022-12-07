install
```shell
kubectl apply -f /local_file/ingress-nginx/v1.5.1/deploy.yaml
```

debug
```shell
kubectl -n ingress-nginx get pod
kubectl -n ingress-nginx logs -f --tail 300 ingress-nginx-controller-x894l
```