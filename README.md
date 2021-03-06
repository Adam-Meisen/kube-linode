## :whale: Provision a Kubernetes / CoreOS Cluster on Linode
[![Bash](https://img.shields.io/badge/language-Bash-green.svg)](https://github.com/kahkhang/kube-linode) [![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/kahkhang/kube-linode/master/LICENSE) [![Twitter](https://img.shields.io/twitter/url/https/github.com/kahkhang/kube-linode.svg?style=social)](https://twitter.com/intent/tweet?text=%23kube-linode%20rocks%21&url=%5Bobject%20Object%5D)

Automatically provision a scalable CoreOS/Kubernetes cluster on Linode with zero configuration.

![Demo](demo.gif)

The cluster will comprise of a single Kubernetes master host with a custom number of worker nodes.

### What's included
* [Self-hosted Kubernetes](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/self-hosted-kubernetes.md) with [Bootkube](https://github.com/kubernetes-incubator/bootkube) using self-hosted etcd
* Load Balancer and automatic SSL/TLS renewal using [Traefik](https://github.com/containous/traefik)
* Two basic auth protected subdomains (assuming you are using example.com):
  * https://kube.example.com ([Kubernetes Dashboard](https://github.com/kubernetes/dashboard))
  * https://traefik.example.com ([Traefik Web UI](https://github.com/containous/traefik#web-ui))
* Distributed block storage with [Rook](https://github.com/rook/rook)

### Usage

```sh
git clone https://github.com/kahkhang/kube-linode
cd kube-linode
chmod +x kube-linode.sh
```

Just run `./kube-linode.sh` into your console, key in your configuration, then sit back and have a :coffee:!

Settings are stored in `settings.env`.

To increase the number of workers, modify `NO_OF_WORKERS` in `settings.env` as desired and run `./kube-linode.sh` again.

Use `kubectl` to control the cluster (e.g. `kubectl get nodes`)

### Dependencies
You should have a Linode account, which you can get [here](https://www.linode.com/?r=0affaec6ca42ca06f5f2c2d3d8d1ceb354e222c1).
You should also have an API Key with a valid domain that uses [Linode's DNS servers](https://www.linode.com/docs/networking/dns/dns-manager-overview#set-domain-names-to-use-linodes-name-servers).

OSX: ``` brew install jq openssl curl kubectl ```

Arch Linux: Follow the instructions [here](https://github.com/kahkhang/kube-linode/issues/4#issuecomment-311601422)


### High Availability Setup
1. Convert a worker node to a master node:
```
kubectl label node $IP "node-role.kubernetes.io/master="
```
2. Scale the etcd operator

### Acknowledgements
This script uses [Bootkube](https://github.com/kubernetes-incubator/bootkube) to bootstrap the initial cluster using [Linode's API](https://www.linode.com/api).
