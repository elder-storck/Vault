# Guia de Instalação do Vault - Linux

Este arquivo contém um guia de instalação manual do Vault para dispositivos Linux. Todas as etapas descritas foram executadas e testadas em uma máquina Ubuntu x64. Para guias de instalação em outros sistemas operacionais, consulte o [Guia de instalaçao do Vault](https://developer.hashicorp.com/vault/tutorials/getting-started/getting-started-install) no site oficial da Hashicorp.

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

### Dica 
Para facilitar o uso do Vault, você pode habilitar o autocompletar de comandos. Isso permitirá que você utilize a tecla Tab para completar comandos do Vault no seu terminal. Para habilitar, execute o seguinte comando:
```bash
sudo apt install <nome_da_ferramenta>
```

Agora que você adicionou o repositório da HashiCorp, também pode instalar outras ferramentas como Terraform, Consul, Nomad e Packer usando o mesmo comando.

```bash
sudo apt install <nome_da_ferramenta>
```