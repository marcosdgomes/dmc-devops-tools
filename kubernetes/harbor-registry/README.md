## Add Helm repo
helm repo 
add harbor https://helm.goharbor.io

## Execute deployment on namespace
helm install harbor harbor/harbor --namespace harbor-system --create-namespace

## Create DB secret for harbor

kubectl create secret generic harbor-db-secret \
  --from-literal=password='your_pwd' \
  -n harbor-system

## Apply Values with real data

helm upgrade harbor harbor/harbor \
  --namespace harbor-system \
  -f values.yaml
  

## Create gcs-key.json
  kubectl create secret generic harbor-gcs-secret \
  --from-file=gcs-key.json=gcs-key.json \
  -n harbor-system