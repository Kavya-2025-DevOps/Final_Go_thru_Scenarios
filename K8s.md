
## K8s scenarios

Scenario Based

**Pod in CrashLoopBackOff **
A pod is continuously restarting. What will you do?


•	Check pod details: “kubectl describe pod <pod-name>” (Look for events, errors)
•	Check logs: “kubectl logs <pod-name>”
•	Check previous logs (important): “kubectl logs <pod-name> --previous” (Because the current container may have already restarted, and might be empty)
•	Validate:
o	Environment variables
o	ConfigMaps / Secrets
o	Application crash
•	Check probes:
o	Liveness / Readiness misconfiguration
•	Resource issues:
o	OOMKilled → increase memory

	I also check if recent deployment caused it and consider rollback.


  
**Rolling Deployment Failure**
New deployment failed. How do you handle?

•	Check rollout status: “kubectl rollout status deployment <name>”
•	Rollback: “kubectl rollout undo deployment <name>”
•	Identify:
o	Image issue
o	Config issue

	I ensure readiness probes prevent bad pods from serving traffic.”

  
**Deployment Stuck in Pending State** 
Pods are not getting scheduled.

•	Check: “kubectl describe pod”
Common reasons:
•	Insufficient resources
•	Node selector mismatch
•	Taints without tolerations


  
**Zero Downtime Deployment Strategy**
How do you ensure zero downtime?
Use rolling updates
•	Configure:
o	maxUnavailable=0
o	maxSurge=1
•	Use readiness probes
Advanced: Blue-Green or Canary deployments

  
**CICD pipeline passed, but production still has old code.**

•	Check pipeline logs: Did deploy stage actually run?
•	Check deploy script: Which environment variable is set?
o	Sometimes, wrong environment — pipeline deployed to Staging not Production.
•	Cache issue: Invalidate CloudFront cache, while using CDN.
o	Browser or CDN is serving cached old version. So, apply a Hard refresh: “Ctrl + Shift + R” — check if new code appears.
•	Health check rollback: Check ALB target group — which version is active?
o	New deployment failed health check, and Load balancer silently rolled back to old version. 
•	Wrong image tag: Never use “:latest” in production.
o	Deployment pulled latest but latest was not updated. Hence, always use specific image tags.
•	Blue-Green switch missed: New version deployed but traffic not switched. Check load balancer listener rules.


  
**High Memory Usage in Pods**
Pods are getting killed due to memory.

•	Check: kubectl top pod
•	Fix:
o	Increase memory limits
o	Optimize application
o	Set proper requests/limits
	Use HPA or VPA depending on use case

  
**Frequent Pod Evictions **
Pods are getting evicted automatically.

•	Node under pressure:
o	Memory
o	Disk
•	Check:
•	kubectl describe node
Fix:
•	Increase node capacity
•	Optimize resource usage

  
**Image Pull Error (ImagePullBackOff) **
Pod cannot pull image.

•	Check:
o	Image name/tag
o	Registry access
o	Credentials
Fix:
•	Use imagePullSecrets

  
**Application Not Accessible in Browser **
App is deployed but not reachable?

Debug Flow:
•	Pod running?
•	Service created?
•	Ingress configured?
Steps:
•	Check pods: “kubectl get pods”
•	Check service: “kubectl get svc”
•	Validate:
o	Correct port mapping
o	Service type (ClusterIP / NodePort / LoadBalancer)
•	If using Ingress:
o	Check ingress rules – (Routing instructions (what to do) eg: define rules - example.com/app1 → goes to app1-service)
o	Check ingress controller – (Traffic manager that applies those instructions (how to do it) eg: NGINX Ingress Controller, AWS ALB Controller)
•	Network policies (if any):

  
**Pods Running but Application Still Failing **
All pods are in Running state, but the application is not working properly.

Note: You understand that Running ≠ Healthy.
Running state only means container is up, not that application is functioning correctly.

Steps:
•	Check logs: “kubectl logs <pod>”
•	Verify readiness probe: 
o	Pod may be running but not ready
•	Check service endpoints: “kubectl get endpoints”
•	Validate DB/API connectivity
•	Check environment variables


  
**Node Not Ready **
Worker node shows NotReady.

•	Check node: “kubectl describe node <node>”
•	Possible causes:
o	Kubelet down
o	Network issue
o	Disk pressure
•	Fix:
o	Restart kubelet
o	Check system logs

  
**Logs Not Available After Pod Restart **
Logs lost after restart.

•	Containers are ephemeral
Solution:
•	Use centralized logging:
o	EFK / ELK stack
o	Cloud logging


