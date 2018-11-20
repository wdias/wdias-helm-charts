# Adapter Scalar - InfluxDB

InfluxDB is a timeseries database with persistance, so, it need to run separately. Further it should be able to use an external InfluxDB server instead of a cluster container.

```
helm install --name adapter-scalar -f values.yaml stable/influxdb
```

### Configurations:
1. https://github.com/helm/charts/blob/master/stable/influxdb/README.md
2. https://github.com/helm/charts/blob/master/stable/influxdb/values.yaml


### NOTES.txt
```
InfluxDB can be accessed via port 8086 on the following DNS name from within your cluster:

- http://adapter-scalar-influxdb.default:8086

You can easily connect to the remote instance with your local influx cli. To forward the API port to localhost:8086 run the following:

- kubectl port-forward --namespace default $(kubectl get pods --namespace default -l app=adapter-scalar-influxdb -o jsonpath='{ .items[0].metadata.name }') 8086:8086

You can also connect to the influx cli from inside the container. To open a shell session in the InfluxDB pod run the following:

- kubectl exec -i -t --namespace default $(kubectl get pods --namespace default -l app=adapter-scalar-influxdb -o jsonpath='{.items[0].metadata.name}') /bin/sh

To tail the logs for the InfluxDB pod run the following:

- kubectl logs -f --namespace default $(kubectl get pods --namespace default -l app=adapter-scalar-influxdb -o jsonpath='{ .items[0].metadata.name }')
```
