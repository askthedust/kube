# Readme

## What certificates upload and where:
- worker nodes:
  - scp ca.pem node-1-key.pem node-1.pem user@node-1
  - scp ca.pem node-2-key.pem node-2.pem user@node-2
- controllers nodes:
  - scp ca.pem ca-key.pem kubernetes-key.pem kubernetes.pem service-account-key.pem service-account.pem user@master-1
  - scp ca.pem ca-key.pem kubernetes-key.pem kubernetes.pem service-account-key.pem service-account.pem user@master-2