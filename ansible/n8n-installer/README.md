# Ansible: n8n Installer

> Playbook para instalar o n8n via Docker, configurado para usar um banco de dados PostgreSQL que já foi criado.

### Pré-requisitos
* Um banco de dados PostgreSQL e um usuário para o n8n já devem existir.

---

### Setup Rápido

#### 1. Crie o Vault com as Credenciais

Dentro desta pasta (`n8n-installer`), crie um arquivo de segredos para o n8n. Ele guardará as credenciais do banco de dados que o n8n precisa para se conectar.

**Comando para criar o cofre:**
```bash
ansible-vault create vars/secrets.yml


# Credenciais para o N8N se conectar ao Postgres
n8n_db_host: "postgres-db"
n8n_db_name: "n8n"
n8n_db_user: "n8n_user"
n8n_db_pass: "SenhaForteParaN8N123!"

# Configuração geral
n8n_timezone: "America/Sao_Paulo"