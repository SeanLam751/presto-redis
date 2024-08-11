Presto Redis Helm Chart
==
This is a helm chart with the following features
- Presto with
    - 1 coordinator node
    - 2 worker nodes
    - A redis connector
- 2 Redis nodes
- 2 rocky linux nodes
- 1 ubuntu node with
    - Presto cli
    - Python 3.8 with pip and redis
    - Java 11 to run presto cli
## Usage
[Helm](https://helm.sh) must be installed to use the charts.

Once helm is installed, add the repo as follows:
```console
helm repo add presto-redis https://trinodb.github.io/charts/
```

To see the charts, run `helm search repo presto-redis`.

Then, you can install the chart with