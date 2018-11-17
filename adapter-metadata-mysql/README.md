# Adapter Metadata - MySQL

MySQL is a persistant database, so, it need to run separately. Further it should be able to use an external MySQL server instead of a cluster container.

```
helm install --name adapter-metadata-mysql -f values.yaml stable/mysql
```

### Configurations:
1. https://github.com/helm/charts/blob/master/stable/mysql/README.md
2. https://github.com/helm/charts/blob/master/stable/mysql/values.yaml


### NOTES.txt
```
MySQL can be accessed via port 3306 on the following DNS name from within your cluster:
adapter-metadata-mysql.default.svc.cluster.local

To get your root password run:

    MYSQL_ROOT_PASSWORD=$(kubectl get secret --namespace default adapter-metadata-mysql -o jsonpath="{.data.mysql-root-password}" | base64 --decode; echo)

To connect to your database:

1. Run an Ubuntu pod that you can use as a client:

    kubectl run -i --tty ubuntu --image=ubuntu:16.04 --restart=Never -- bash -il

2. Install the mysql client:

    $ apt-get update && apt-get install mysql-client -y

3. Connect using the mysql cli, then provide your password:
    $ mysql -h adapter-metadata-mysql -p

To connect to your database directly from outside the K8s cluster:
    MYSQL_HOST=127.0.0.1
    MYSQL_PORT=3306

    # Execute the following command to route the connection:
    kubectl port-forward svc/adapter-metadata-mysql 3306

    mysql -h ${MYSQL_HOST} -P${MYSQL_PORT} -u root -p${MYSQL_ROOT_PASSWORD}
    e.g.: mysql -h 127.0.0.1 -uwdias -p
```
