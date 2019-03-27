# Adapter - Redis

Redis is a NoSQL database based on Memory, so, it need to run separately. Further it should be able to use an external Redis instance instead of a cluster container.

```
helm install --name adapter-redis -f values.yaml stable/redis
```

### Configurations:
1. https://github.com/helm/charts/blob/master/stable/redis/README.md
2. https://github.com/helm/charts/blob/master/stable/redis/values.yaml


### NOTES.txt
```sh
NOTES:
** Please be patient while the chart is being deployed **
Redis can be accessed via port 6379 on the following DNS name from within your cluster:

adapter-redis.default.svc.cluster.local


To get your password run:

    export REDIS_PASSWORD=$(kubectl get secret --namespace default adapter-redis -o jsonpath="{.data.redis-password}" | base64 --decode)

To connect to your Redis server:

1. Run a Redis pod that you can use as a client:

   kubectl run --namespace default adapter-redis-client --rm --tty -i --restart='Never' \
    --env REDIS_PASSWORD=$REDIS_PASSWORD \
   --image docker.io/bitnami/redis:4.0.12 -- bash

2. Connect using the Redis CLI:
   redis-cli -h adapter-redis -a $REDIS_PASSWORD

To connect to your database from outside the cluster execute the following commands:

    export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
    export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services adapter-redis-master)
    redis-cli -h $NODE_IP -p $NODE_PORT -a $REDIS_PASSWORD
```

#### Database allocation
0 - adapter-metadata
1 - extension-scheduler / adapter-extension
2 - adapter-status

### Dev Support
- `kubectl get pods | grep 'redis' | awk '{print $1}' | xargs -o -I {} kubectl exec -it {} -- /bin/bash`
- `redis-cli -h 127.0.0.1 -p 6379 -n <DB_NUMBER> -a <PASSWORD>`
