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

```sh
helm repo add elasticsearch https://helm.elastic.co
helm pull elasticsearch/elasticsearch
tar -xzf elasticsearch-8.5.1.tgz 
helm install elasticsearch ./elasticsearch --values ./elasticsearch/values.yaml --namespace dhuo-core --create-namespace 
helm uninstall elasticsearch -n dhuo-core 
kubectl port-forward service/elasticsearch-cluster-master 9200:9200 --namespace dhuo-core
```

```sh
helm repo add superset https://apache.github.io/superset
helm pull superset/superset
tar -xzf superset-0.12.6.tgz
helm install superset ./superset --values ./superset/values.yaml --namespace production --create-namespace 
helm uninstall superset -n production
k port-forward service/superset 8088:8088 -n production
```
