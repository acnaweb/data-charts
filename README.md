# Data Charts

## Instalação -  Amundsen no K8S

#### Chart

```sh
helm pull dhuodata/amundsen --version 0.0.3
```

#### Values

| key | value |
| -- | --| 
| search.imageTag | 2.11.1 |
| metadata.imageTag | 3.9.0 |
| frontEnd.imageTag | 3.12.0 |
| neo4j.imageTag | 3.5.26 |
| search.proxy.endpoint | elasticsearch-cluster-master.dhuo-core.svc.cluster.local:9200 |
| search.proxy.user | elastic |
| search.proxy.password | <secret> |

#### Metadata - Criar usuário

Criar port-forward para o service `amundsen-metadata`

```sh
kubectl port-forward service/amundsen-metadata 5002:5002 --namespace dhuo-core 
```

Criar o usuário 

```sh
curl -X PUT -v http://localhost:5002/user \
-H "Content-Type: application/json" \
--data \
'{"user_id":"test_user_id","first_name":"test","last_name":"user", "email":"test_user_id@mail.com"}'
```

```sh
helm repo add dhuodata https://registry-dhuo.br.engineering/chartrepo/helm-data
helm pull dhuodata/amundsen
tar -xzf amundsen-v0.0.3.tgz
helm install amundsen ./amundsen --values ./amundsen/values.yaml --namespace dhuo-core --create-namespace 
helm uninstall amundsen --namespace dhuo-core 
kubectl port-forward service/amundsen-frontend 5000:5000 --namespace dhuo-core
kubectl port-forward service/amundsen-neo4j 7474:7474 --namespace dhuo-core
kubectl port-forward service/amundsen-neo4j 7473:7473 --namespace dhuo-core
kubectl port-forward service/amundsen-neo4j 7687:7687 --namespace dhuo-core 
kubectl port-forward service/amundsen-metadata 5002:5002 --namespace dhuo-core 

```

## Instalação - ElasticSearch no K8S

#### Chart

```sh
helm repo add elasticsearch https://helm.elastic.co
helm pull elasticsearch/elasticsearch --version 7.17.3
tar -xzf elasticsearch-8.5.1.tgz 
helm install elasticsearch ./elasticsearch --values ./elasticsearch/values.yaml --namespace dhuo-core --create-namespace 
helm uninstall elasticsearch -n dhuo-core 
kubectl port-forward service/elasticsearch-cluster-master 9200:9200 --namespace dhuo-core
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
