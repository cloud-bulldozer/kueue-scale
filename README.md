# Kueue Perf & Scale testing

## Kueue deployment

Kueue upstream can be deployed in OCP with

```shell
oc apply --server-side -f https://github.com/kubernetes-sigs/kueue/releases/download/v0.10.1/manifests.yaml
```

[Kueue operator](https://github.com/openshift/kueue-operator) is also available  and is now the recommended way to deploy Kueue.


## Workloads available

- Jobs: Deploys plain pods at scale in `kueue-scale` namespace. These pods are assigned to the namespace's LocalQueue
- Pods: Deploys jobs at scale in the `kueue-scale` namespace. These pods are assigned to the namespace's LocalQueue
- Multi-queue: Deploys jobs at scale across 10 namespaces prefixed with `kueue-scale`. The LocalQueues assigned to the jobs belong to the same cohort.

## Prometheus queries

Apart from kube-burner's jobLatency and podLatency measurements, we also collect a series of metrics from Prometheus.
Stored in [kueue-metrics.yml](e2e/kueue-metrics.yml)
