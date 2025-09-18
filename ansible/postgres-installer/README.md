# 🚀 Ansible: PostgreSQL Installer & Manager

> Playbook para instalar o PostgreSQL e gerenciar múltiplos bancos de dados de forma segura e idempotente, utilizando o **Ansible Vault** para proteger as senhas.

### Estrutura de Arquivos
* `inventory.ini`: Lista dos servidores.
* `install-postgres.yml`: O playbook principal.
* `vars/secrets.yml`: **Arquivo criptografado** contendo as senhas e nomes de bancos/usuários.

### Setup e Gerenciamento (com Ansible Vault)

#### Passo 1: Configure o Inventário (`inventory.ini`)
Este arquivo agora contém apenas os IPs dos seus servidores.

```ini
[servers]
# IP do seu servidor aqui
167.86.90.233 ansible_user=root


## Como executar
ansible-playbook -i inventory.ini install_postgres.yml --ask-vault-pass
ansible-playbook -i inventory.ini install_postgres_docker.yml --ask-vault-pass


## Para atualizar secrets
ansible-vault edit vars/secrets.yml

Para adicionar um novo banco, basta adicicionar as novas infos na lista.