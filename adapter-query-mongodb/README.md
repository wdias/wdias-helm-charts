# Adapter Query - MongoDB

MongoDB is a persistant database, so, it need to run separately. Further it should be able to use an external MongoDB server instead of a cluster container.

```
helm install --name adapter-query-mongodb -f values.yaml stable/mongodb
```

# NOTES:
```sh
** Please be patient while the chart is being deployed **

MongoDB can be accessed via port 27017 on the following DNS name from within your cluster:

    adapter-query-mongodb.default.svc.cluster.local

To get the root password run:

    export MONGODB_ROOT_PASSWORD=$(kubectl get secret --namespace default adapter-query-mongodb -o jsonpath="{.data.mongodb-root-password}" | base64 --decode)

To get the password for "wdias" run:

    export MONGODB_PASSWORD=$(kubectl get secret --namespace default adapter-query-mongodb -o jsonpath="{.data.mongodb-password}" | base64 --decode)

To connect to your database run the following command:

    kubectl run --namespace default adapter-query-mongodb-client --rm --tty -i --restart='Never' --image bitnami/mongodb --command -- mongo admin --host adapter-query-mongodb --authenticationDatabase admin -u root -p $MONGODB_ROOT_PASSWORD

To connect to your database from outside the cluster execute the following commands:

    kubectl port-forward --namespace default svc/adapter-query-mongodb 27017:27017 &
    mongo --host 127.0.0.1 --authenticationDatabase admin -p $MONGODB_ROOT_PASSWORD
```
