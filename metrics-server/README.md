# metrics-server
metrics-server needs to install in order to get resource usage data.
https://kubernetes.io/docs/tasks/debug-application-cluster/core-metrics-pipeline/#metrics-server

`helm install --name metrics-server --namespace=kube-system stable/metrics-server -f ~/wdias/wdias-helm-charts/metrics-server/values.yaml`

wdias-data-collector is using native go-client (e.g. https://github.com/kubernetes/client-go/blob/master/examples/in-cluster-client-configuration/main.go) with;
`kubectl create clusterrolebinding default-cluster-admin --clusterrole=cluster-admin --serviceaccount=default:default`

# NOTES:
```
The metric server has been deployed.

In a few minutes you should be able to list metrics using the following
command:

  kubectl get --raw "/apis/metrics.k8s.io/v1beta1/nodes"
```
