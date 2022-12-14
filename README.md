# Howto

## Setup Cluster

Go to <https://my.vultr.com/kubernetes/add/> for:

- Cluster Name: `private-infra-cluster`
- Kubernetes Version (at time of writing): v1.24.3+2
- Cluster Location: Frankfurt
- Cluster Capacity (node pool):
  - Label: `pool-1`
    - Node Pool Type: `Regular Cloud Compute`
    - 1 CPU, 2 GiB RAM, 55 GiB storage, 2000 GB bandwidth
    - 3 nodes

(Note: you may dowload the specific cluster config to some `vke-*.yaml` and activate it in bash with `export KUBECONFIG=<FILE>`)

### Estimated Monthly Cost:

- three nodes: $30
- static IP (load balancer): $10

## Deploy

- for static IP, see [static-ip-svc.yaml](kustomization/base/static-ip-svc.yaml)
  (this is a separate service, so the actual load balancer, e.g. nginx, can be cycled without loosing the static IP;
  see <https://kubernetes.github.io/ingress-nginx/examples/static-ip/> or <https://github.com/kubernetes/ingress-nginx/tree/main/docs/examples/static-ip>)
- for nginx loadbalancer from <https://artifacthub.io/packages/helm/ingress-nginx/ingress-nginx>,
  see the helm chart section in [base/kustomization.yaml](kustomization/base/kustomization.yaml)

**Problem** here the nginx still uses an own IP instead of the static IP

Deploy (apply) the configuration with:

```
kubectl kustomize kustomization/base --enable-helm | kubectl apply -f -
```

**Dangerous** Rollback (delete) configuration with:

```
kubectl kustomize kustomization/base --enable-helm | kubectl delete -f -
```
