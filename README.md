# Monitoring-Stack: Out of the Box Monitoring and Logging for k8s

  

**Components**: Grafana, Prometheus, Loki, Node Exporter, Promtail

Monitoring stack is a simple solution helm-based solution to get started with monitoring k8s workloads and components as well as collect and centralized logs for easy query

Monitoring-stack is an out of the box solution that has a provisioned dashboard and is easily extensible to add more components.

  

## Pre-requisites:

  

- Kube-state-metrics : if not present on cluster,
Set parameter **global.metrics.present** to **True** in values file 


- Helm: Config, scripts are written in helm files. If not present on cluster [Install Helm](https://helm.sh/docs/intro/install/)

  

## Deployment:

To **deploy** monitoring-stack on local, test and general environments(not cloud-specific), Run:

    helm install <Release name> monitoring-stack --set global.env.local=true


This creates a helm release comprising a monitoring namespace and all the components within it without persistent volumes.

**Deploying to AWS environments with EBS backed volumes for data persistence, Run:** 

    helm install <Release name> monitoring-stack --set global.env.aws=true


#
  

To check that components are deployed and working as expected,

  

    kubectl get pods -w -n monitoring

  

Metrics and Log visualization is available via **Grafana** on < node ip >:31500 (default) or localhost:31500 for single node clusters.

  

Grafana nodeport can be altered in the values.yaml file if need be.

  

To **delete** monitoring-stack,

  

helm uninstall < Release name >

  

## Monitoring:

K8s and node metrics are collected via various datsources: node-exporter, kube_state_metrics etc and scraped by a Prometheus server.

Prometheus is highly customizable and its config file can be altered for a optimal use case.

  

Data is Visualized via Grafana and a provisioned community dashboard as shown below:

  
  

![Grafana Dashboard](https://lh3.googleusercontent.com/pw/AM-JKLV7rJW_0QcJ-_yPBeg3be_9yrxRVa53UYSxse1174vxEZFfCYZATKW1EG7R7XOWfYVF1z2vbYHbjWAhMDJoN9aDO9PNJY_X9TTThw-yscqBW4npG2D9NlrqY08vwaz017TvCjYyZxv4Tt7pLxb13WmZNw=w2551-h1364-no?authuser=0)

  
  
  

## Logging:

Loki is a lightweight log aggregation system and integrates natively with the rest of the prometheus-grafana stack and a wide range of data sources. Monitoring-stack incorporates loki and data from a promtail daemonset.

  
  

![Loki Logs](https://lh3.googleusercontent.com/pw/AM-JKLXtcucSa_967m_MGXXINdxSrhLZ0LLV1Wcgv21UVQvLmJfgGm0WIDrKIPJ38kgyh9hdwXop1iglS0SUW8UXqs1FPhEM6H5qYlSTvCpJjRirI9VXLLn2slTB4of7sJfu3YEXHTX9YLF42LDqoF9iJrnqFA=w2554-h1375-no?authuser=0)