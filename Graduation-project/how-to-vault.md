downland the CSI drivers from the docs
download the vault drivers for vault docs (helm)
add the vault CA to the vault daemonSet 
configure the StorageClass



on vault:
go to access modes add k8s and 
add the k8s CA
and create the issuer token for the vault
click on the Disable use of local CA and service account JWT
kubectl create token vault-reviewer -n bridgex --duration=720h
config a role inside it 

also in my case the CSI secrets driver needed a permission so i added secrets-store-csi-driver-secret-role


For policies:
path "secret/data/bridgex/db" {
  capabilities = ["read"]
}

# Allow reading the specific secret you are asking for
path "bridgex/data/db" {
  capabilities = ["read"]
}

# Just in case it's a KV Version 1 engine, add this too:
path "bridgex/db" {
  capabilities = ["read"]
}


path "secret/data/bridgex/backend" {
  capabilities = ["read"]
}

# Allow reading the specific secret you are asking for
path "bridgex/data/backend" {
  capabilities = ["read"]
}

# Just in case it's a KV Version 1 engine, add this too:
path "bridgex/backend" {
  capabilities = ["read"]
}
