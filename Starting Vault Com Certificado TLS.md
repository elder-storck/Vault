# Instalando o Vault com Certificado TLS
## Copiando o Certificado e Criando Diretórios

#### Step 1: Criando as Pastas

Antes de iniciar a instalação, é necessário criar os diretórios onde o Vault armazenará os dados e os certificados TLS. Execute o seguinte comando:
```bash
mkdir -p /opt/vault/{tls,data}
```
#### Step 2: Copiando o Certificado para o Servidor

Caso esteja acessando o servidor via SSH, utilize o comando scp para copiar o certificado TLS. Substitua <IP_DO_SERVIDOR> pelo IP real do seu servidor e os nomes dos arquivos conforme necessário:
```bash
scp meuCertificado.crt root@<IP_DO_SERVIDOR>:/opt/vault/tls/
scp meuCertificado.key root@<IP_DO_SERVIDOR>:/opt/vault/tls/
```



## Verificando e definindo permissões aos Certificados.

Após a cópia, confirme se os certificados estão no diretório correto executando:
```bash
ls -l /opt/vault/tls/
```
Verifique e defina as permissões corretas para os certificados:
```bash
chown vault: /opt/vault/tls/*
```
⚠️ **Atenção:** Certifique-se de que o certificado tenha as permissões corretas. Consulte a documentação adicional, se necessário.




## Criando o arquivo de configuração
Crie e edite o arquivo de configuração do Vault:
```bash
nano  /etc/vault/config.hcl
```
Adicione o seguinte conteúdo ao arquivo:
```bash
storage "file" {
  path    = "./vault/data"
}

listener "tcp" {
  address     = "0.0.0.0:8200"
  tls_cert_file = "/opt/vault/tls/meuCertificado.crt"
  tls_key_file = "/opt/vault/tls/meuCertificado.key"
}

ui = true
```



## Iniciando e Verificando o Serviço Vault
Inicie o serviço do Vault:
```bash
service vault start
```
Verifique se ele está rodando corretamente:
```bash
service vault status
```
Caso precise instalar utilitários de rede para verificar conexões, instale o pacote net-tools:
```bash
apt install net-tools
```
Para verificar se o Vault está escutando na porta correta, use:
```bash
netstat -plant | grep vault
```



## Configurando Variáveis de Ambiente
Defina o endereço do Vault para uso nas próximas interações:
```bash
export VAULT_ADDR='https://<hostname>:8200'
```
Especifique o certificado para comunicação segura:
```bash
export VAULT_CACERT="/opt/vault/tls/meuCertificado.crt"
```




## Inicializando o Vault
Agora, inicialize o Vault:
```bash
vault status
```
```bash
vault operator init
```
