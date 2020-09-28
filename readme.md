# Readme

## What certificates upload and where:
- worker nodes:
  - scp ca.pem node-1-key.pem node-1.pem user@node-1
  - scp ca.pem node-2-key.pem node-2.pem user@node-2
- controllers nodes:
  - scp ca.pem ca-key.pem kubernetes-key.pem kubernetes.pem service-account-key.pem service-account.pem user@master-1
  - scp ca.pem ca-key.pem kubernetes-key.pem kubernetes.pem service-account-key.pem service-account.pem user@master-2

## Copy configs to nodes
- worker nodes:
  - scp node-1.kubeconfig kube-proxy.kubeconfig user@node-1:/home/user/
  - scp node-2.kubeconfig kube-proxy.kubeconfig user@node-2:/home/user/
- controller nodes:
  - scp admin.kubeconfig kube-controller-manager.kubeconfig kube-scheduler.kubeconfig user@master-1
  - scp admin.kubeconfig kube-controller-manager.kubeconfig kube-scheduler.kubeconfig user@master-2

## Copy the encryption-key to controller nodes:
- scp encryption-config.yml user@master-1
- scp encryption-config.yml user@master-2