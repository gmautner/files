```bash
git clone https://github.com/gmautner/files.git
cd files
helm repo add cilium https://helm.cilium.io/
chmod +x ./create-kubernetes-binaries-iso.sh
```

```bash
# Consultar versões cri-tools em https://github.com/kubernetes-sigs/cri-tools/releases
export KUBE_VERSION=1.30.9
export CILIUM_VERSION=1.16.6
export CRICTL_VERSION=1.30.1
```

```bash
helm template cilium/cilium --version $CILIUM_VERSION --kube-version $KUBE_VERSION \
  -f cilium_values.yaml \
  --namespace kube-system \
  > cilium-v$CILIUM_VERSION+k8s-v$KUBE_VERSION.yaml
```

```bash
cat cilium-v$CILIUM_VERSION+k8s-v$KUBE_VERSION.yaml > network.yaml
cat node-updater.yaml >> network.yaml
```

```bash
./create-kubernetes-binaries-iso.sh ./ $KUBE_VERSION 1.6.2 $CRICTL_VERSION file://$(pwd)/network.yaml https://raw.githubusercontent.com/kubernetes/dashboard/v2.6.1/aio/deploy/recommended.yaml k8s-v$KUBE_VERSION+cilium-v$CILIUM_VERSION
```
