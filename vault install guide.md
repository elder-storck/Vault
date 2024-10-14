# Guia de Instalação do Vault - Linux

A HashiCorp mantém e assina pacotes oficialmente para as seguintes distribuições Linux.

Siga as instruções no [Guia Oficial de Empacotamento](https://www.hashicorp.com) para instalar a chave GPG da HashiCorp, verificar a impressão digital da chave e instalar o Vault.

## Passos de Instalação

### 1. Atualize o gerenciador de pacotes e instale GPG e wget

```bash
sudo apt update && sudo apt install gpg wget
```

### 2. Baixe o keyring

```bash
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
```

### 3. Verifique o keyring

```bash
gpg --no-default-keyring --keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg --fingerprint
```

### 4. Adicione o repositório da HashiCorp

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
```

### 5. Instale o Vault

```bash
sudo apt update && sudo apt install vault
```

### Nota
Para instalar o Vault Enterprise, substitua install vault por install vault-enterprise.

### Dica
Agora que você adicionou o repositório da HashiCorp, também pode instalar outras ferramentas como Terraform, Consul, Nomad e Packer usando o mesmo comando.

```bash
sudo apt install <nome_da_ferramenta>
```
