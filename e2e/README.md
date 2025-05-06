# E2E performance workloads

## Jobs

Creates k8s jobs in the `kueue-scale-<size>` namespace throughput 4 different stages:

- Small: 20 replicas with parallelism 5 -> 100 pods
- Medium: 100 replicas with parallelism 5 -> 500 pods
- Large: 200 replicas with parallelism 5 -> 1000 pods
- Extra Large: 400 replicas with parallelism 5 -> 2000 pods

It also creates:

- 1 ResourceFlavor
- 1 ClusterQueue
- 1 LocalQueue per namespace
  
Kueue can be toggled with the variable `kueue` in [jobs/config.yml](jobs/config.yml)

### Metrics

The metrics for the jobs can be found in [e2e/metrics.yml](e2e/metrics.yml)
