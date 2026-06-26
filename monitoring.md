
## Monitoring
1. How do you automate Grafana alert acknowledgment?

   Grafana does not directly support automatic alert acknowledgment as a core concept. In practice, alerts are either auto-resolved when the metric condition returns to normal, or suppressed using silences via Alertmanager during maintenance or deployments. For production incident management, Grafana alerts are integrated with tools like PagerDuty or ServiceNow, where acknowledgment and lifecycle management of incidents are handled.

   
2. How do you send Kubernetes metrics to Grafana?  
   Grafana itself does not collect metrics from Kubernetes. Prometheus scrapes metrics from Kubernetes components and       applications. Grafana queries Prometheus and visualizes the data.  
   The common architecture is:  
   Kubernetes Cluster → Prometheus (scrapes metrics) → Grafana (dashboards) → Alertmanager (alerts)  

3. What data source does Grafana use for Kubernetes metrics?
   Grafana uses Prometheus as the primary data source. Prometheus scrapes Kubernetes metrics from nodes, pods, and applications at regular intervals (typically 15–30 seconds). Grafana queries Prometheus and displays the metrics on dashboards in near real time.
   eg: CPU usage; Memory usage; Pod restarts; Request rate; API latency
   Kubernetes -> Prometheus -> Grafana
   
4. How do you send container logs to Grafana?  
   Container logs are collected using Promtail or Fluent Bit and sent to Loki. Grafana uses Loki as the data source to query and visualize the logs.
   eg: Application logs; Error logs; Container stdout/stderr logs; Kubernetes pod logs.
   Kubernetes -> Promtail/Fluent Bit -> Loki -> Grafana



5. what type of alerts have configured and How ?

   Alerts I configured:  

      High CPU usage (e.g., >80% for 5 minutes)  
      High memory utilization  
      Pod in CrashLoopBackOff  
      Pod restart count exceeds a threshold  
      Node NotReady  
      Disk usage above 85–90%  
      Application downtime (service unavailable)  
      High HTTP 5xx error rate  
      High API response latency  
   
6. what type of Dashboards have you configured and How ?  
   Kubernetes cluster health (node status, CPU, memory, disk usage)  
   Pod and container metrics (CPU, memory, restarts, pod status)  
   Application dashboards (request rate, response time, error rate, throughput)  
   Infrastructure dashboards (server utilization, filesystem usage, network traffic)

7. How I configured them:

   Prometheus scraped metrics from Kubernetes nodes, pods, and applications using ServiceMonitors.  
   Grafana was configured with Prometheus as the data source.  
   I created dashboards using PromQL queries to visualize key metrics.  
   I defined alert rules in Grafana (or Prometheus Alertmanager, depending on the environment) with thresholds and evaluation periods.  
   I configured notification channels such as email, Slack, or Microsoft Teams so alerts were sent to the operations team when thresholds were exceeded.

8. 
   

