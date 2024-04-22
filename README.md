# Data Charts

Deploy data services on Kubernetes

## Airbyte

```sh
helm repo add airbyte https://airbytehq.github.io/helm-charts
```

```sh
helm install airbyte airbyte/airbyte
```

## Amundsen

#### Metadata - Criar usuário

Criar port-forward para o service `amundsen-metadata`

```sh
kubectl port-forward service/amundsen-metadata 5002:5002 --namespace data 
```

Criar o usuário 

```sh
curl -X PUT -v http://localhost:5002/user \
-H "Content-Type: application/json" \
--data \
'{"user_id":"test_user_id","first_name":"test","last_name":"user", "email":"test_user_id@mail.com"}'
```

```sh
helm repo add XXXX
helm pull amundsen
helm install amundsen ./amundsen --values ./amundsen/values.yaml --namespace data--create-namespace 
helm uninstall amundsen --namespace data
kubectl port-forward service/amundsen-frontend 5000:5000
kubectl port-forward service/amundsen-neo4j 7474:7474
kubectl port-forward service/amundsen-neo4j 7473:7473
kubectl port-forward service/amundsen-neo4j 7687:7687 
kubectl port-forward service/amundsen-metadata 5002:5002 

```

## Instalação - ElasticSearch no K8S

#### Chart

```sh
helm repo add elasticsearch https://helm.elastic.co
helm pull elasticsearch/elasticsearch --version 7.17.3
tar -xzf elasticsearch-8.5.1.tgz 
helm install elasticsearch ./elasticsearch --values ./elasticsearch/values.yaml --namespace data --create-namespace 
helm uninstall elasticsearch -n data 
kubectl port-forward service/elasticsearch-cluster-master 9200:9200 --namespace data
```

## Instalação - Superset

```sh
helm repo add superset https://apache.github.io/superset
helm pull superset/superset
tar -xzf superset-0.12.6.tgz
helm install superset ./superset --values ./superset/values.yaml --namespace production --create-namespace 
helm uninstall superset -n production
k port-forward service/superset 8088:8088 -n production
```
