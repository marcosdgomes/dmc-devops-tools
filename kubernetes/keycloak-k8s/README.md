# QIAM Kubernetes Manifests

Este diretório contém os manifestos Kubernetes para o QIAM, usando Kustomize para gerenciar diferentes ambientes.

## Estrutura

```
kubernetes/
├── base/                      # Configurações base
│   ├── qiam-deployment.yaml   # Deployment do QIAM
│   ├── qiam-service.yaml      # Service do QIAM
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
kubectl -n qiam-ee-poc create secret docker-registry regcred \
  --docker-server=registry.konneqt.io \
  --docker-username='<USUARIO>' \
  --docker-password='<SENHA>' \
  --docker-email='marcos@konneqt.io'

### Aplique ao namespace
kubectl -n qiam-ee-poc patch deploy qiam \
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

## Acessando o QIAM

- HTTP: `http://qiam.local:8080`
- HTTPS: `https://qiam.local:8443`

## Configurações

### Banco Local
- Database: `keycloak`
- Usuário: `keycloak`
- Senha: `keycloak`
- URL: `jdbc:postgresql://postgres:5432/keycloak`

### Admin QIAM
- Usuário: `admin`
- Senha: `admin`

## Volumes Persistentes

O banco de dados local usa um PVC de 1Gi. Ajuste `postgres-pvc.yaml` se precisar de mais espaço.
