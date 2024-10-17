# Vault Installation and Management Guides

Este repositório contém uma coleção de guias detalhados sobre como instalar e gerenciar o Vault, uma solução segura para o gerenciamento de senhas e segredos.

O Vault opera em dois modos principais: dev mode (modo de desenvolvimento) e production mode (modo de produção). No dev mode, o sistema é carregado inteiramente na memória principal, sendo recomendado apenas para testes e aprendizado da ferramenta. Este tutorial, no entanto, foca na configuração do Vault para ambientes de produção.

No modo de produção, o Vault pode ser configurado sem TLS (não recomendado por questões de segurança) ou com um certificado TLS. É altamente recomendável que, para ambientes de produção, o Vault seja sempre configurado com TLS, garantindo uma camada extra de proteção. Mesmo em ambientes de desenvolvimento, o uso de TLS é encorajado para criar um ambiente mais seguro.


## Conteúdo
1. [Vault installation guide](./vault_installation_guide.md)
2. [Starting the Vault server without TLS](./starting_the_Vault_server_without_TLS.md)

<!-- 
  2. [Configuração Inicial do Vault](./configuracao-inicial.md)
3. [Gerenciamento de Tokens e Políticas](./gerenciamento-tokens-politicas.md)
4. [Integração do Vault com Aplicações](./integracao-aplicacoes.md)
5. [Backup e Recuperação no Vault](./backup-recuperacao.md)
6. [Melhores Práticas de Segurança no Vault](./melhores-praticas-seguranca.md) 
-->


Sinta-se à vontade para explorar os guias e contribuir com melhorias ou sugestões.
