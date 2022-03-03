# Monitoring-Stack: Out of the Box Monitoring and Logging for k8s 

**Components**: Grafana, Prometheus, Loki, Node Exporter, Promtail
 
 Monitoring stack is a simple solution helm-based solution to get started with monitoring k8s workloads and components as well as collect and centralized logs for easy query
 Monitoring-stack is an out of the box solution that has a provisioned dashboard and is easily extensible to add more components...Happy helming.

## Pre-requisites:

 - K8s Metric server: if not present on cluster, run `kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml`
 - Helm: Config, scripts are written in helm files. If not present on cluster [Install Helm](https://helm.sh/docs/intro/install/)  

## Deployment:
To **deploy** monitoring-stack, Run:

    helm install <Release name> monitoring-stack
    # Creates a monitoring namespace and deploys all the components within it 

To check that components are deployed and working as expected, 

    kubectl get pods -n monitoring

Metrics and Log visualization is available via **Grafana** on < node ip >:31500 (default) or localhost:31500 for single node clusters.

Grafana nodeport can be altered in the values.yaml file if need be.

To **delete** monitoring-stack,

    helm uninstall < Release name >

## Monitoring:
K8s and node metrics are collected via various datsources: node-exporter, kube_state_metrics etc and scraped by a Prometheus server.
Prometheus is highly customizable and its config file can be altered for a optimal use case.

Data is Visualized via Grafana and a provisioned community dashboard as shown below:


![Grafana Dashboard](https://photos.google.com/share/AF1QipPsXMn0o3agiVE3p4mpiAeNctQSrQ5WS1vInwxPcajVOeMwDEhbGvNrZJcFKgqNqg/photo/AF1QipNBBdZqdCjY7MNd0GcRq9mfSUYB9JAPU4Va53yz?key=WVN3bXVoaXhIME5PWnY2blNTOGtWNTJGZ29oM2lB)



##  Logging: 
Loki is a lightweight log aggregation system and integrates natively with the rest of the prometheus-grafana stack and a wide range of data sources. Monitoring-stack incorporates loki and data from a promtail daemonset.

sharing
![Loki Logs](https://photos.google.com/share/AF1QipPsXMn0o3agiVE3p4mpiAeNctQSrQ5WS1vInwxPcajVOeMwDEhbGvNrZJcFKgqNqg/photo/AF1QipPA81xSMHyImPPdTc46ArVkTCcsVVqyctpVD2lC?key=WVN3bXVoaXhIME5PWnY2blNTOGtWNTJGZ29oM2lB)