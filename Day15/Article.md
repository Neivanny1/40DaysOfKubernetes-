# Day 15/40 - Mastering Node Affinity in Kubernetes 🚀

<img src='./assets/15.png'>

As I move forward with the #40daysofkubernetes challenge, today’s focus was on Kubernetes Node Affinity—a feature that allows for sophisticated pod scheduling based on node labels. Here’s an overview of what I learned about Node Affinity and how it differs from basic Node Selectors.

## 🔍 Beyond Node Selectors: Introducing Node Affinity

While Node Selectors allow simple pod placement based on node labels, Node Affinity offers greater flexibility and control over pod scheduling. With Node Affinity, I can specify exact conditions for where my pods should or should not be placed, providing precise management over pod locations within the Kubernetes cluster.

## Node Affinity Types 🔑 requiredDuringSchedulingIgnoredDuringExecution:
1. Strict Placement: Ensures that pods only schedule on nodes with specified labels.
2. No Runtime Checks: Labels aren’t checked after the pod is running, so if a node’s labels change, the pod remains in place.

## preferredDuringSchedulingIgnoredDuringExecution:
1. Preferred Placement: This rule sets “preferences” for node selection. If no nodes meet these preferences, Kubernetes still schedules the pod to the best match available.

## Practical Example: Node Affinity with Required Scheduling

Suppose my application requires high-speed storage. I can use Node Affinity to target nodes labeled with disktype=ssd.

Sample YAML Configuration:
```
#yaml

apiVersion: v1
kind: Pod
metadata:
  name: redis-pod
  labels:
    app: redis
spec:
  containers:
  - name: redis
    image: redis
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: disktype
            operator: In
            values:
            - ssd
```

In this example, Kubernetes schedules the redis-pod only on nodes labeled with disktype=ssd, ensuring it has access to high-speed storage.
## 📝 Task 15/40 - Exploring Node Affinity

For today’s task, I worked through the following steps:

1. Created a pod with Node Affinity: I used nginx as the image, with a requiredDuringSchedulingIgnoredDuringExecution rule for disktype=ssd.
2. Labeling Nodes: Initially, the pod was unscheduled. After labeling worker-node1 with disktype=ssd, the pod deployed successfully.
3. Configured a Redis Pod with Open Node Affinity: For this step, I used a Redis image with a more flexible Node Affinity rule and labeled worker-node2 with disktype but no specific value. As expected, the pod scheduled to worker-node2.

## 💡 Key Takeaways
1. Node Affinity provides more precise scheduling controls than Node Selectors, allowing specific placement needs for pods.
requiredDuringSchedulingIgnoredDuringExecution enables strict node affinity for pods but does not enforce it after the pod is placed on a node.
2. Adding Labels Dynamically: By adding or removing labels on nodes, it’s possible to control pod scheduling dynamically.

## 📺 Video Reference

For a deep dive into today’s concepts, check out the Day 15 video on Kubernetes Node Affinity:

[![Day15/40 - Kubernetes node affinity explained](https://img.youtube.com/vi/5vimzBRnoDk/sddefault.jpg)](https://youtu.be/5vimzBRnoDk)

Node Affinity is a powerful tool for applications that have specific hardware or storage requirements, allowing targeted pod placement. With this feature, I can more effectively manage resource allocation in the Kubernetes environment.

[@Eric mwakazi](https://www.linkedin.com/in/eric-mwakazi), [@PiyushSachdeva](https://www.linkedin.com/in/piyush-sachdeva) and [@CloudOps Community](https://www.linkedin.com/company/thecloudopscomm)
#40daysofkubernetes #Kubernetes #DaemonSet #Job #CronJob #DevOps #ContainerOrchestration #NodeAffinity 