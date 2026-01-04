I will use TrueNAS NFS cause i want RWX and ISCSI doesn't support it

Following this tutorial https://jonathangazeley.com/2021/01/05/using-truenas-to-provide-persistent-storage-for-kubernetes/
## Installation
### Prepare nodes
Install nfs utils:
sudo apt install libnfs-utils

### Install CSI 
Prepare helm:
helm repo add democratic-csi https://democratic-csi.github.io/charts/
helm repo update
helm search repo democratic-csi/


wget https://raw.githubusercontent.com/democratic-csi/charts/master/stable/democratic-csi/examples/freenas-nfs.yaml


helm upgrade \
--install \
--create-namespace \
--values csi-freeNas.yaml \
--namespace democratic-csi \
zfs-nfs democratic-csi/democratic-csi