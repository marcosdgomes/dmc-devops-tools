# Ansible: Docker + Portainer

> Um playbook pra subir um servidor Ubuntu do zero com Docker e Portainer CE. É idempotente.

### Intro

* Instala o **Docker Engine** direto do repo oficial
* Sobe versão do **Portainer CE** indicada no .inv da raíz;
* Permite configurar a **versão do Portainer** e a **senha inicial do admin** direto no inventário.
* Adiciona seu usuário ao grupo `docker`(para não expor `sudo`).

### Requisitos

1.  **Ansible** instalado.
2.  **Acesso SSH** e SSH keys configuradas.

### Como usar

1.  **Clone o projeto.**

2.  **Ajuste o `inventory.ini`:**
    Coloque o IP do seu servidor e, se quiser, defina a versão e a senha do Portainer.

    ```ini
    [servers]
    # IP do seu servidor aqui
    192.168.1.10

    [portainer:children]
    servers

    [portainer:vars]
    portainer_version=2.33.1
    
    # Opcional: define a senha inicial do usuário 'admin'
    portainer_initial_password=TEMP_PWD
    ```

3.  **Rode o playbook:**

    ```bash
    ansible-playbook -i inventory.ini install_portainer.yml
    ```

### Acesso

* Acesse o Portainer em: `https://<IP_DO_SEU_SERVIDOR>:9443`
