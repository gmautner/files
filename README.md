```bash
./create-kubernetes-binaries-iso.sh ./ 1.30.9 1.6.2 1.30.1 https://raw.githubusercontent.com/gmautner/files/main/cilium-1.16.6.yaml https://raw.githubusercontent.com/kubernetes/dashboard/v2.6.1/aio/deploy/recommended.yaml setup-v1.30.9+cilium-1.16.6
```

```bash
helm template cilium/cilium --version 1.16.6 \
  -f cilium_values.yaml \
  --namespace kube-system \
  > cilium-1.16.6.yaml
```
