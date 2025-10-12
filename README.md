### Home Task 1

Disable option `--cloud-provider=external` for `kubelet`, `kube-apiserver` and `kube-controller-manager`.  
After that nginx container was able to start.

### Home task 2.1

- Added static pod manifests for etcd, kube-apiserver, kube-controller-manager, and kube-scheduler.

- Disabled manual startup of these components in setup.sh — they are now launched automatically by kubelet as static pods.

- Increased the maxPods parameter for kubelet from 4 to 40.

### Home task 2.2 (Kube-apiserver profiling)

- Create cluster
- run container with kubectl-flame (file kubectl-flame-pod.yaml)
- find kube-apiserver PID on codespace node (It doesn't work with `kubectl debug` way if kube-apiserver runs as a static pod)

  ```bash
  pgrep kube-apiserver

  ```
- run perf record generation:

  ```bash
  sudo kubebuilder/bin/kubectl exec kubectl-flame -- perf record -F 99 -g -p 9041 -o /tmp/out -- sleep 30
  ```
- create graph

  ```bash
  sudo kubebuilder/bin/kubectl exec kubectl-flame -- sh -c "/app/perf script -i /tmp/out | /app/FlameGraph/stackcollapse-perf.pl | /app/FlameGraph/flamegraph.pl > /tmp/flame.svg"
  ```
- copy graph file to localhost

  ```bash
  sudo kubebuilder/bin/kubectl cp kubectl-flame:/tmp/flame.svg /workspaces/mastering-k8s/kube-apiserver-flame.svg
  ```

- 
