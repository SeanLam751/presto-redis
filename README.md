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
To make the mongo database work, 
