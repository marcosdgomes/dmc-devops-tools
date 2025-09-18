# Ansible: Nginx Proxy Manager

> Playbook para instalar o Nginx Proxy Manager (NPM) via Docker em um servidor Ubuntu. Ele sobe o container e já libera as portas `80`, `443` e `81` no firewall `UFW`.

### Setup Rápido

1.  **Ajuste o `inventory.ini` com o IP do seu servidor:**

    ```ini
    [servers]
    # IP do seu servidor aqui
    167.86.90.233 ansible_user=root
    ```

2.  **Rode o playbook:**

    ```bash
    ansible-playbook -i inventory.ini install_npm.yml
    ```

### Primeiro Acesso

* **URL:** `http://<IP_DO_SEU_SERVIDOR>:81`
* **Login Padrão:**
    * **Email:** `admin@example.com`
    * **Senha:** `changeme`
* (Você precisará trocar a senha ao entrar pela primeira vez).