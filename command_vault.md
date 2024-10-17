# Criando o certificado
step 1: Criando as pastas
```bash
mkdir -p /opt/vault/{tls,data}
```
step 2: em `opt/vault/tls` vamos criar o certificado com a função open ssl, com duração de 10 anos, no campo `subjectAltName` é necesario informar o IP da máquina e o nome da maquina configurado no DNS.
```bash
cd /opt/vault/tls
```
```bash
openssl req -out tls.crt -new -keyout tls.key -newkey rsa:4096 -nodes -sha256 -x509 -subj "/O=HashiCorp/CN=Vault" -addext "subjectAltName = IP:0.0.0.0,DNS:vault-server.local" -days 3650
```
## Verificando a criação dos certificados.

Verificando se os cerificados foram criados.
```bash
ls -l   #listas os certificados
```

Se não tiver nenhum nome para maquina configurado no DNS, vá em `/etc/hosts ` e adiciona a seguinte linha no final do arquivo.
```bash
127.0.0.1 vault-server.local
```
**Nota:** O nome da máquina pode ser qualquer um, desde de que seja o nome que foi inserido na criação do certificado.

```bash
ping -c 4 vault-server.local
```

## Instalando o Vault
Seguir o tutorial de instalação, tutorial pode ser encontrado neste mesmo repositorio, ou na pagina oficial da Hashicorp(adicionar o link).
## Criando o arquivo de configuração
```bash
nano  /etc/vault/config.hcl
```
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
```bash
chown vault: /opt/vault/tls/*
```
```bash
service vault start
```
```bash
vault status
```

```bash
apt install net-tools
```

```bash
netstat -plant | grep vault
```

```bash
export VAULT_ADDR='http://<hostname>:8200'
```

```bash
export VAULT_CACERT="/opt/vault/tls/tls.crt"

```

```bash
vault status
```
```bash
vault init
```
