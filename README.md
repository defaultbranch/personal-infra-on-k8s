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