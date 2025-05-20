# Kueue Perf & Scale testing


## Kueue deployment

Kueue can be deployed in OCP with

```shell
oc apply --server-side -f https://github.com/kubernetes-sigs/kueue/releases/download/v0.10.1/manifests.yaml
```

[Kueue operator](https://github.com/openshift/kueue-operator) is also available  and is now the recommended way to deploy Kueue.


## Prometheus queries


```yaml
# Jobs

- query: count(kube_job_info{namespace=~"kueue-scale-.+"})
  metricName: totalJobs

- query: sum(kube_pod_status_phase{namespace=~"kueue-scale-.+"}) by (phase)
  metricName: podStatusCount > 0

- query: avg(kube_job_status_completion_time{namespace=~"kueue-scale-.+"} - kube_job_status_start_time{namespace=~"kueue-scale-.+"}) by (namespace)
  metricName: avgJobCompletionTime

- query: quantile(0.90,kube_job_status_completion_time{namespace=~"kueue-scale-.+"} - kube_job_status_start_time{namespace=~"kueue-scale-.+"}) by (namespace)
  metricName: p90JobCompletionTime


# Pod CPU & memory

- query: (sum(irate(container_cpu_usage_seconds_total{name!="",container!="POD",namespace=~"kueue-system|openshift-kube-scheduler|openshift-kube-apiserver"}[2m])) by (pod,namespace)) > 0
  metricName: kueueCPUUsage

- query: (sum(container_memory_working_set_bytes{name!="",container!="POD",namespace=~"kueue-system|openshift-kube-scheduler|openshift-kube-apiserver"}) by (pod,namespace)) > 0
  metricName: kueueMemoryUsage
 ```
