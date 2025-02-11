```bash
git clone https://github.com/gmautner/files.git
cd files
helm repo add cilium https://helm.cilium.io/
chmod +x ./create-kubernetes-binaries-iso.sh
```

```bash
export CILIUM_VERSION=1.16.6
helm template cilium/cilium --version $CILIUM_VERSION \
  -f cilium_values.yaml \
  --namespace kube-system \
  > cilium-$CILIUM_VERSION.yaml
```

```bash
cat cilium-$CILIUM_VERSION.yaml > network.yaml
cat node-updater.yaml >> network.yaml
```

```bash
./create-kubernetes-binaries-iso.sh ./ 1.30.9 1.6.2 1.30.1 file://$(pwd)/network.yaml https://raw.githubusercontent.com/kubernetes/dashboard/v2.6.1/aio/deploy/recommended.yaml k8s-v1.30.9
```
