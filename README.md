### Home Task 1

Disable option `--cloud-provider=external` for `kubelet`, `kube-apiserver` and `kube-controller-manager`.  
After that nginx container was able to start.

### Hometask 2.1

- Added static pod manifests for etcd, kube-apiserver, kube-controller-manager, and kube-scheduler.

- Disabled manual startup of these components in setup.sh — they are now launched automatically by kubelet as static pods.

- Increased the maxPods parameter for kubelet from 4 to 40.