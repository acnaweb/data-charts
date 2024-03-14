helm repo add dhuodata https://registry-dhuo.br.engineering/chartrepo/helm-data
helm pull dhuodata/amundsen
tar -xzf amundsen-v0.0.3.tgz
helm install amundsen ./amundsen --values ./amundsen/values.yaml --namespace dhuo-core --create-namespace 
helm uninstall amundsen --namespace dhuo-core 

helm repo add elasticsearch https://helm.elastic.co
helm pull elasticsearch/elasticsearch
tar -xzf elasticsearch-8.5.1.tgz 
helm install elasticsearch ./elasticsearch --values ./elasticsearch/values.yaml --namespace dhuo-core --create-namespace 
helm uninstall elasticsearch


kubectl port-forward service/amundsen-frontend 5000:5000 --namespace dhuo-core
kubectl port-forward service/amundsen-neo4j 7474:7474 --namespace dhuo-core
kubectl port-forward service/amundsen-neo4j 7473:7473 --namespace dhuo-core
kubectl port-forward service/amundsen-neo4j 7687:7687 --namespace dhuo-core 
kubectl port-forward service/elasticsearch-cluster-master 9200:9200 --namespace dhuo-core



