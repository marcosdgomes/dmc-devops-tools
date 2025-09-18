# keycloak Kubernetes Manifests

Este diretório contém os manifestos Kubernetes para o keycloak, usando Kustomize para gerenciar diferentes ambientes.

## Estrutura

```
kubernetes/
├── base/                      # Configurações base
│   ├── keycloak-deployment.yaml   # Deployment do keycloak
│   ├── keycloak-service.yaml      # Service do keycloak
│   └── kustomization.yaml     # Kustomization base
├── overlays/                  # Variantes de configuração
│   ├── local-db/             # Configuração com banco local
│   │   ├── postgres-*.yaml   # Manifestos do PostgreSQL
│   │   ├── configmap.yaml    # ConfigMap com configs locais
│   │   ├── secret.yaml       # Secrets com credenciais
│   │   └── kustomization.yaml
│   └── remote-db/            # Configuração com banco remoto
│       ├── configmap.yaml    # ConfigMap com configs remotas
│       ├── secret.yaml       # Secrets com credenciais
│       └── kustomization.yaml
```

## Como usar



### Com banco de dados local

```bash
# Criar namespace
kubectl create namespace <your_namespace>

### Registre o docker registry para o namespace
kubectl -n keycloak-ee-poc create secret docker-registry regcred \
  --docker-server=registry.dmc-it-solutions.io \
  --docker-username='<USUARIO>' \
  --docker-password='<SENHA>' \
  --docker-email='marcos@dmc-it-solutions.io'

### Aplique ao namespace
kubectl -n keycloak-ee-poc patch deploy keycloak \
  -p '{"spec":{"template":{"spec":{"imagePullSecrets":[{"name":"regcred"}]}}}}'

# Aplicar configuração com banco local
kubectl apply -k overlays/local-db
```

### Com banco de dados remoto

1. Edite `overlays/remote-db/configmap.yaml` e configure a URL do banco:
   ```yaml
   KC_DB_URL: "jdbc:postgresql://seu-banco-remoto:5432/keycloak"
   ```

2. Edite `overlays/remote-db/secret.yaml` e configure as credenciais:
   ```yaml
   KC_DB_USERNAME: "seu-usuario"
   KC_DB_PASSWORD: "sua-senha"
   ```

3. Aplique a configuração:
   ```bash
   kubectl apply -k overlays/remote-db
   ```

## Acessando o keycloak

- HTTP: `http://keycloak.local:8080`
- HTTPS: `https://keycloak.local:8443`

## Configurações

### Banco Local
- Database: `keycloak`
- Usuário: `keycloak`
- Senha: `keycloak`
- URL: `jdbc:postgresql://postgres:5432/keycloak`

### Admin keycloak
- Usuário: `admin`
- Senha: `admin`

## Volumes Persistentes

O banco de dados local usa um PVC de 1Gi. Ajuste `postgres-pvc.yaml` se precisar de mais espaço.
