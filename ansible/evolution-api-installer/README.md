# 🚀 Ansible: Evolution API Installer

> Playbook para instalar a Evolution API e seu banco de dados MongoDB via Docker.

### Setup Rápido

1.  **Crie o Vault com as Credenciais**

    Use `ansible-vault create vars/secrets.yml` e defina a chave da API e a senha do MongoDB.

    **Conteúdo de Exemplo para `vars/secrets.yml`:**
    ```yaml
    evolution_api_key: "SuaChaveDeAPISuperSecreta123!"
    mongodb_root_user: "root"
    mongodb_root_password: "SuaSenhaForteParaO-MongoDb456!"
    ```

2.  **Ajuste o `inventory.ini`** com o IP do seu servidor.

3.  **Rode o Playbook** com a senha do seu cofre (vault).
    ```bash
    ansible-playbook -i inventory.ini install_evolution_api.yml --ask-vault-pass
    ```

### Como Usar

* A API estará disponível em: `http://<IP_DO_SEU_SERVIDOR>:8080`
* Para interagir com a API, você precisará passar a `AUTHENTICATION_API_KEY` que você definiu no seu vault.
* **Dica:** Use o Nginx Proxy Manager para dar à sua API um domínio com SSL (ex: `https://api.seusite.com.br`).