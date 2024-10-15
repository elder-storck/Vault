# A Guide to Utilizing HashiCorp Vault in Production

## Step 1: Create a Configuration File

To begin, create a configuration file with the `.hcl` extension. Use the following command:

```bash
nano config.hcl
```
Inside the config.hcl file, add the following content:

```bash
storage "raft" {
  path    = "./vault/data"
  node_id = "node1"
}

listener "tcp" {
  address     = "127.0.0.1:8200"
  tls_disable = "true"
}

api_addr = "http://127.0.0.1:8200"
cluster_addr = "https://127.0.0.1:8201"
ui = true
```

- The `storage` section defines where Vault's data will be stored, in this case at `./vault/data` (a directory we will create later).
- The `listener` section configures Vault to listen on the local IP `127.0.0.1` at port `8200`. TLS is disabled for this local setup (`tls_disable = "true"`).
- The UI interface is enabled (`ui = true`), allowing access through a browser.

**Note:** TLS (Transport Layer Security) is a cryptographic protocol used to secure communications over a network. Although we are disabling it for this local setup, **it is essential to enable TLS in a real production environment** to ensure secure communication between Vault and its clients.

## Step 2: Create "RAFT" Storage Backend Directory

Next, create the directory where Vault's "RAFT" storage backend will store its data:

```bash
mkdir -p ./vault/data
```

## Step 3: Start the Vault Server Using the Configuration File

Start the Vault server with the configuration we created earlier (`config.hcl`):
```bash
vault server -config=config.hcl
```

## Step 4: Export the VAULT_ADDR Environment Variable

Vault needs to know where the server is running. Set the `VAULT_ADDR` environment variable to point to the server address:
```bash
export VAULT_ADDR='http://127.0.0.1:8200'
```

## Step 5: Initialize Vault

Before Vault can be used, it needs to be initialized. This generates the keys needed to unseal and manage Vault:
```bash
vault operator init
```

## Step 6: Unseal Vault

After initialization, Vault will be sealed. You need to unseal it using the keys provided during initialization:


## Tip: Enable Command Autocomplete

To make using Vault easier, you can enable command autocomplete for Vault. This will allow you to tab-complete Vault commands in your shell. To enable it, run the following command:
```bash
vault -autocomplete-install
```









