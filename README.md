helm repo add dhuodata https://registry-dhuo.br.engineering/chartrepo/helm-data
helm pull dhuodata/amundsen
tar -xzf amundsen-v0.0.3.tgz
helm install amundsen ./amundsen --values ./amundsen/values.yaml
helm uninstall amundsen

helm repo add elasticsearch https://helm.elastic.co
helm pull elasticsearch/elasticsearch
tar -xzf elasticsearch-8.5.1.tgz 
helm install elasticsearch ./elasticsearch --values ./elasticsearch/values.yaml 
helm uninstall elasticsearch

kubectl port-forward service/amundsen-frontend 5000:5000