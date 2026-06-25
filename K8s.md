## K8s

1. How do you identify which microservice deployment failed?  
   "kubectl get deployments  
    kubectl rollout status deployment/<deployment-name> "

2. How do you send Kubernetes metrics to Grafana?
   Grafana itself does not collect metrics from Kubernetes. Prometheus scrapes metrics from Kubernetes components and       applications. Grafana queries Prometheus and visualizes the data.
   The common architecture is:
   Kubernetes Cluster → Prometheus (scrapes metrics) → Grafana (dashboards) → Alertmanager (alerts)
   
   
