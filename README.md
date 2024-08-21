Presto Mongo Helm Chart
==
This is a helm chart with the following features
- Presto with
    - 1 coordinator node
    - 2 worker nodes
    - A redis and mongo connector
- 2 Redis nodes
- 1 Mongo node
- 2 rocky linux nodes
- 1 ubuntu node with
    - Presto cli
    - Java 11 to run presto cli
- 1 python job to populate the redis node with data
## Usage
[Helm](https://helm.sh) must be installed to use the charts.

It is recommended to configure more memory for the kubernetes cluster. Presto is relatively memory hungry. This helm chart is confirmed to work with 7gb of memory.

Once helm is installed, add the repo as follows:
```console
helm repo add presto-redis https://seanlam751.github.io/presto-redis/
```

To see the charts, run `helm search repo presto-redis`.

Then, you can install the chart with
```console
helm install presto-redis presto-redis/presto-redis
```
To make the mongo database work, the storage needs to be given the label `nodeAffinity=default`. On minikube, you can grant the label like so:
```console
kubectl label nodes minikube nodeAffinity=default
```
In addition, the database does not have a functional automatic script. To add data to the database, use the following commands to `kubectl exec -it pod/mongodb-replica-0 -- /bin/bash`
```js
rs.initiate({
    _id: "rs0",
    members: [
        { _id: 0, host: "mongodb-replica-0.mongo-service.default.svc.cluster.local:27017" }
    ]
    });

    // Create a collection and insert some documents
    // do not name the database with any capital letter
    db.testcollection.insertMany([
      { name: "Alice", age: 30 },
      { name: "Bob", age: 25 },
      { name: "Carol", age: 35 }
    ]);

    print("Database initialized with test data.");
```

To connect to presto, first find the name of the ubuntu deployment with `kubectl get pod -l app=ubuntu-deployment`
Then, connect to ubuntu instance with `kubectl exec -it <ubuntu-name> -- /bin/bash`
Then search for the cluster ip with `kubectl get svc presto-redis`
Finally, connect to presto using `./presto --server <cluster-ip>:8080`