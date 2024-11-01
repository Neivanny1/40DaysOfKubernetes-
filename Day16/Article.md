# Day 16/40 - Mastering Kubernetes Resource Requests and Limits 🚀🔧

<img src='./assets/16.png'>

Welcome to Day 16 of our Kubernetes journey! Today, we’re diving into Requests and Limits, essential Kubernetes configurations that enable efficient resource management, ensuring pods operate smoothly without causing disruptions in the cluster. This article complements our video guide on Requests and Limits. Let’s unpack how to make the most of these settings and why they’re crucial for optimal Kubernetes performance.

## 🏙️ Requests and Limits: Resource Management Simplified

In Kubernetes, pods are like tenants in a bustling apartment building (our cluster). Each tenant requires specific resources, like CPU and memory, to operate. Requests and Limits play a key role here:

1. Requests are the minimum amount of resources a pod requires to function. Think of it as the base reservation that each pod needs.
2. Limits define the maximum resources a pod can use. It acts as a cap, ensuring that no pod consumes more than its fair share, which could otherwise disrupt neighboring pods.

This balance is essential for resource control and predictable performance.

## 🧐 Why Requests & Limits Matter

1. Resource Control: Limits prevent a single pod from consuming excessive resources, reducing the risk of out-of-memory (OOM) kills and CPU starvation.
2. Predictability: Requests enable the Kubernetes scheduler to allocate resources efficiently, maintaining smooth operation across the cluster.
3. Stability: Setting limits prevents critical resource shortages that could impact the overall system stability.

## 🛠️ Practical Example: Memory Requests and Limits

In our video, we demonstrate these concepts in action with practical examples. Here’s a look at how you can use Requests and Limits in Kubernetes to manage resources effectively.

## Exceeding Available Memory: The OOM Scenario

Let’s say we have a pod that requests 50Mi of memory but has a limit of 100Mi. If the pod uses more than this, it will be terminated due to an OOM error, as shown below:
```
#yaml

apiVersion: v1
kind: Pod
metadata:
  name: memory-demo-2
  namespace: mem-example
spec:
  containers:
  - name: memory-demo-2-ctr
    image: polinux/stress
    resources:
      requests:
        memory: "50Mi"
      limits:
        memory: "100Mi"
    command: ["stress"]
    args: ["--vm", "1", "--vm-bytes", "250M", "--vm-hang", "1"]
```
This OOM termination is actually a helpful safeguard, ensuring that the pod doesn’t consume all resources and affect other workloads.
Successfully Scheduled Pod

To better illustrate resource management, here’s another pod that requests 100Mi of memory with a 200Mi limit, and this will run smoothly:
```
#yaml

apiVersion: v1
kind: Pod
metadata:
  name: memory-demo
  namespace: mem-example
spec:
  containers:
  - name: memory-demo-ctr
    image: polinux/stress
    resources:
      requests:
        memory: "100Mi"
      limits:
        memory: "200Mi"
    command: ["stress"]
    args: ["--vm", "1", "--vm-bytes", "150M", "--vm-hang", "1"]
```

## 📝 Applying Requests & Limits
1. Create a Namespace: Log into your cluster and create a new namespace called mem-example.
2. Install Metrics Server: Follow the Kubernetes documentation for detailed setup.
3. Run Example Pods: Implement and observe the effects of Requests and Limits with the YAML configurations above.

## 🎓 Key Takeaways

1. Requests define the minimum resources a pod needs, while Limits cap the maximum it can use.
2. Correctly configuring Requests and Limits maintains resource efficiency, ensures cluster stability, and helps prevent system issues.
3. Using the Kubernetes metrics server, you can monitor resource usage and refine these configurations over time.

## 🌐 Join the Discussion

[@Eric mwakazi](https://www.linkedin.com/in/eric-mwakazi), [@PiyushSachdeva](https://www.linkedin.com/in/piyush-sachdeva) and [@CloudOps Community](https://www.linkedin.com/company/thecloudopscomm)
#40daysofkubernetes #Kubernetes #DaemonSet #Job #CronJob #DevOps #ContainerOrchestration #NodeAffinity 