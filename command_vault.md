mkdir -p /opt/vault/{tls,data}
cd /opt/vault/tls
openssl req -out tls.crt -new -keyout tls.key -newkey rsa:4096 -nodes -sha256 -x509 -subj "/O=HashiCorp/CN=Vault" -addext "subjectAltName = IP:0.0.0.0,DNS:vault-server.local" -days 3650

In /opt/vault/tls
    ls -l   #listas os certificados
    openssl x509 -in tls.crt -noout -t

IN /etc/hosts 
    adicionar a linha "127.0.0.1 vault-server.local"

ping -c 4 vault-server.local



nano  /etc/vault/config.hcl
```bash
storage "file" {
  path    = "./vault/data"
}

listener "tcp" {
  address     = "0.0.0.0:8200"
  tls_cert_file = "/opt/vault/tls/tls.crt"
  tls_key_file = "/opt/vault/tls/tls.key"
}

ui = true
```

chown vault: /opt/vault/tls/*

service vault start
