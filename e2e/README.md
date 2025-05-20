# E2E performance workloads

## Jobs

Creates k8s jobs in the `kueue-scale-<size>` namespace throughput 4 different stages, tracking job latency through the `jobLatency` measurement.

- Small: 20 replicas with parallelism 5 -> 100 pods
- Medium: 100 replicas with parallelism 5 -> 500 pods
- Large: 200 replicas with parallelism 5 -> 1000 pods
- Extra Large: 400 replicas with parallelism 5 -> 2000 pods

It also creates:

- 1 ResourceFlavor
- 1 ClusterQueue
- 1 LocalQueue per namespace
  
Kueue can be toggled with the variable `kueue` in [jobs/config.yml](jobs/config.yml)

## Pods

Creates 2k plain pods in the `kueue-scale-xl` namespace, it also tracks pod ready latency using kube-burner's `podLatency` measurement.

It also creates:

- 1 ResourceFlavor
- 1 ClusterQueue
- 1 LocalQueue

Similar to the Jobs workload, Kueue can be toggled with the variable `kueue` in [pods/config.yml](pods/config.yml)

### Metrics

The metrics for these workloads can be found in [metrics.yml](metrics.yml)
