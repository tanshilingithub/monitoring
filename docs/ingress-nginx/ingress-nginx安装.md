install
```shell
kubectl apply -f /local_file/ingress-nginx/v1.5.1/deploy.yaml
```

debug
```shell
kubectl -n ingress-nginx get pod -o wide
kubectl -n ingress-nginx logs -f --tail 300 ingress-nginx-controller-jprkp
kubectl -n ingress-nginx delete pod ingress-nginx-controller-4skc6 ingress-nginx-controller-lmxsz
```