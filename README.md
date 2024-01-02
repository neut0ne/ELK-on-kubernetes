Start:
```
podman machine set -cpus 4 -m 8192
podman machine start
minikube start --driver=podman
minikube status
kubectl cluster-info

helm repo add elastic https://Helm.elastic.co
helm repo list

curl -O https://raw.githubusercontent.com/elastic/Helm-charts/master/elasticsearch/examples/minikube/values.yaml
helm install elasticsearch elastic/elasticsearch -f ./elasticsearch-values.yaml
kubectl get pods
kubectl get svc
```

In separate terminal:
```
kubectl port-forward svc/elasticsearch-master 9200

Helm install kibana elastic/kibana
kubectl get pods
```

In another separate terminal:
```
kubectl port-forward deployment/kibana-kibana 5601
```

See Kibana in browser:
```
localhost:5601
```

Install metricbeat
```
helm install --name metricbeat elastic/metricbeat
kubectl get pods
```

See indexed metrics in elasticsearch:
```
curl localhost:9200/_cat/indices
```

GUI part. 
Go to kibana in browser. 

management > stack management > kibana > index patterns > create index pattern > for name, type metricbeat* > for timestampfield, choose @timestamp

Index pattern fields are populating.

Go to "discover" and stretch time range to see metrics data. 

