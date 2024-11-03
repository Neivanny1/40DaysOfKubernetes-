# Day 18/40 - Health Probes in Kubernetes: Liveness, Readiness, and Startup Explained 🩺

<img src='./assets/18.png'>

Today’s focus was on Health Probes in Kubernetes—a vital feature for maintaining application reliability and self-healing capabilities within a cluster. Kubernetes probes ensure that applications are healthy and responsive, automatically restarting or waiting on pods if health checks fail. Here’s a summary of what I learned about Kubernetes health probes and the steps I followed to apply them in my cluster.

## 🛠 Task Overview
### 1. Creating Pods with Health Probes:
#### Busybox Pod with Liveness Probe:
1. Created a pod with the registry.k8s.io/busybox image.

2. Added a liveness probe using the command cat /tmp/healthy, with a check frequency of every 5 seconds and an initial delay of 5 seconds. This probe helps determine if the pod is healthy by checking for the existence of /tmp/healthy.
3. Agnhost Pod with HTTP Liveness and Readiness Probes:
4. Deployed a second pod using the registry.k8s.io/e2e-test-images/agnhost:2.40 image.
5. Configured HTTP liveness and readiness probes to check the /healthz path on port 8080, starting after an initial delay of 5 seconds and every 10 seconds thereafter.

#### 2. Testing Health Probe Functionality:
Observed Kubernetes automatically restarting pods based on the probe results.

By setting probes, we can manage pods efficiently, ensuring they’re either serving requests or restarting when necessary.

## 📘 Key Takeaways on Health Probes
Types of Health Probes:

### Liveness Probe:
Checks if a container is running. If it fails, Kubernetes restarts the container.

## Use Case: Helps recover from unresponsive states.

### Readiness Probe:
Determines if a container is ready to serve requests. If it fails, the pod is removed from the Service endpoints.
## Use Case: Ensures traffic only reaches healthy pods, maintaining application availability.

### Startup Probe:
Primarily for legacy applications needing additional time to start. It signals Kubernetes when the container is fully started and ready for other probes.

## Use Case: Ensures long-startup applications aren’t prematurely terminated.

## Types of Health Check Methods:
1. HTTP: Accesses a specified URL to verify health.
2. TCP: Opens a TCP socket to check availability.
3. Command: Executes a specified command; the probe succeeds if it returns a 0 status.

## Practical Application

Health probes are essential for monitoring applications and ensuring reliability, especially in large, production-grade environments. Probes automatically manage container restarts and limit network traffic to healthy containers, reducing downtime and improving application stability.

## 📺 Video Reference For an in-depth walkthrough, check out the Day 18 video on Kubernetes Health Probes.
[![Day 18/40 - Health Probes in kubernetes](https://img.youtube.com/vi/x2e6pIBLKzw/sddefault.jpg)](https://youtu.be/x2e6pIBLKzw)


## SHARING

What insights do you have about using Kubernetes health probes? Feel free to share your thoughts, and don’t forget to tag [@Eric mwakazi](https://www.linkedin.com/in/eric-mwakazi), [@PiyushSachdeva](https://www.linkedin.com/in/piyush-sachdeva) and [@CloudOps Community](https://www.linkedin.com/company/thecloudopscomm)

#40daysofkubernetes #Kubernetes #HealthProbes #DevOps #CloudComputing #ApplicationStability #SelfHealing