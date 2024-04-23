https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-certs/#kubelet-serving-certs

Enabling signed kubelet serving certificates
By default the kubelet serving certificate deployed by kubeadm is self-signed. This means a connection from external services like the metrics-server to a kubelet cannot be secured with TLS.

To configure the kubelets in a new kubeadm cluster to obtain properly signed serving certificates you must pass the following minimal configuration to kubeadm init:

apiVersion: kubeadm.k8s.io/v1beta3
kind: ClusterConfiguration
---
apiVersion: kubelet.config.k8s.io/v1beta1
kind: KubeletConfiguration
serverTLSBootstrap: true
If you have already created the cluster you must adapt it by doing the following:

Find and edit the kubelet-config ConfigMap in the kube-system namespace. In that ConfigMap, the kubelet key has a KubeletConfiguration document as its value. Edit the KubeletConfiguration document to set serverTLSBootstrap: true.
On each node, add the serverTLSBootstrap: true field in   and restart the kubelet with systemctl restart kubelet

kubectl edit configmap kubelet-config -n kube-system

add serverTLSBootstrap: true

kubectl get csr
kubectl certificate approve <CSR-name>

#Not Recomended
Enable insecure security tls 
Add helm variable --set args="{--kubelet-insecure-tls}"