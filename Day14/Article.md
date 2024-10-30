# Day 14/40 - Taints and Tolerations in Kubernetes 📘🚀
<img src='./assets/14.png'>

As I continue with the #40daysofkubernetes challenge, today's exploration focused on Taints and Tolerations—crucial concepts for managing pod scheduling in Kubernetes. Here’s an overview of what I learned and how I implemented these tools.

## 🔍 Understanding Taints

Taints act like "only you are allowed" signs on your Kubernetes nodes. By marking nodes with specific characteristics (e.g., "gpu=true"), taints prevent pods from being scheduled on them unless those pods have the necessary permissions—known as tolerations. This helps control where workloads run, ensuring efficient resource utilization.
## Key Use Cases for Taints:
1. Reserving nodes for specific workloads (e.g., GPU-accelerated applications).
2. Protecting system nodes from unwanted pod scheduling.
3. Enforcing rules around node utilization.

## Sample Command for Tainting a Node

To taint a node, I used the following command:
```
kubectl taint nodes node1 key=gpu:NoSchedule
```
This command prevents pods without a toleration for this taint from being scheduled on node1.
🕒 Exploring Tolerations in Kubernetes

>>Tolerations allow pods to "tolerate" taints, letting them bypass scheduling restrictions. By defining tolerations in the pod specification, I can ensure that specific pods can be scheduled on tainted nodes.

### Example YAML for Adding Toleration to a Pod

```
#yaml

apiVersion: v1
kind: Pod
metadata:
  labels:
    run: redis
  name: redis
spec:
  containers:
  - image: redis
    name: redis
  tolerations:
  - key: "gpu"
    operator: "Equal"
    value: "true"
    effect: "NoSchedule"
```
>Note: This YAML allows the pod to be scheduled on nodes tainted with the "gpu" key.

## 🧭 Combining Taints, Tolerations, and Node Affinity

While taints and tolerations are powerful, they have limitations. They don't support complex expressions (like "AND" or "OR"). In such cases, combining taints, tolerations, and node affinity can provide a more flexible scheduling strategy.

## 💡 Key Takeaways
1. Taints help control where pods can be scheduled, ensuring resources are used efficiently.
2. Tolerations allow specific pods to bypass taint restrictions.
3. Combining taints, tolerations, and node affinity offers more control over pod scheduling.

## 📺 Video Reference

To explore these concepts further, check out the Day 14 video on Taints and Tolerations in Kubernetes:

Day 14/40 - Taints and Tolerations in Kubernetes
Practical Application of Today’s Learnings
[![Day14/40 - Taints and Tolerations in Kubernetes](https://img.youtube.com/vi/nwoS2tK2s6Q/sddefault.jpg)](https://youtu.be/nwoS2tK2s6Q)


Today's insights are essential for fine-tuning pod scheduling and ensuring optimal resource utilization across Kubernetes clusters. By mastering taints and tolerations, I can more effectively manage workloads and improve the overall efficiency of my deployments.

[@Eric mwakazi](https://www.linkedin.com/in/eric-mwakazi), [@PiyushSachdeva](https://www.linkedin.com/in/piyush-sachdeva) and [@CloudOps Community](https://www.linkedin.com/company/thecloudopscomm)
#40daysofkubernetes #Kubernetes #DaemonSet #Job #CronJob #DevOps #ContainerOrchestration