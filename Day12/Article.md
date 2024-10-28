# Day 12/40 - Mastering DaemonSets, Jobs, and CronJobs in Kubernetes 🚀

<img src='./assets/12.png'>

As I progress through the #40daysofkubernetes challenge, today's topic covered DaemonSets, Jobs, and CronJobs—essential components for managing Kubernetes workloads efficiently. Here’s what I learned and the steps I took to implement these concepts.

## 🔍 Understanding DaemonSets

A DaemonSet is a specialized Kubernetes object designed to ensure a pod runs on every node within a cluster. Unlike a Deployment that scales pods based on replicas, DaemonSets deploy one pod per available node by default, making them ideal for deploying infrastructure-related services across the cluster.
## Key Use Cases for DaemonSets:
1. Network proxies: kube-proxy
2. Cluster networking solutions: calico, weave-net
3. Monitoring agents: node monitoring and logging

## Example YAML for DaemonSet

Here’s a sample YAML to create a DaemonSet named nginx-ds, which deploys nginx on every node.

```
#daemonset.yaml

apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: nginx-ds
  labels:
    env: demo
spec:
  template:
    metadata:
      labels:
        env: demo
      name: nginx
    spec:
      containers:
      - image: nginx
        name: nginx
        ports:
        - containerPort: 80
  selector:
    matchLabels:
      env: demo
```

## 🕒 Exploring CronJobs in Kubernetes

A CronJob allows you to run jobs on a scheduled basis using cron syntax. For instance, I created a simple CronJob that prints "40daysofkubernetes" every 5 minutes, utilizing the busybox image.
### Sample YAML for CronJob
```
#cronjob.yaml

apiVersion: batch/v1
kind: CronJob
metadata:
  name: print-message
spec:
  schedule: "*/5 * * * *"  # every 5 minutes
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: print-container
            image: busybox
            args:
            - /bin/sh
            - -c
            - "echo 40daysofkubernetes"
          restartPolicy: OnFailure
```
## 💡 Key Takeaways
1. DaemonSets are invaluable for managing system-level tasks across all nodes.
2. Jobs run discrete tasks, useful for one-off operations.
3. CronJobs schedule tasks, which is ideal for periodic processes.

## 📺 Video Reference

To dive deeper into today’s concepts, watch the Day 12 video on DaemonSets, Jobs, and CronJobs: 

Day12/40 - Kubernetes Daemonset Explained

[![Day12/40 - Kubernetes Daemonset Explained - Daemonsets, Job and Cronjob in Kubernetes](https://img.youtube.com/vi/kvITrySpy_k/sddefault.jpg)](https://youtu.be/kvITrySpy_k)

## Practical Application of Today’s Learnings

DaemonSets are indispensable when you need consistent functionality on all nodes, and Jobs or CronJobs are excellent for tasks like backups or scheduled data processing. These tools help automate and simplify workload management in a Kubernetes cluster.

Tags

[@Eric mwakazi](https://www.linkedin.com/in/eric-mwakazi), [@PiyushSachdeva](https://www.linkedin.com/in/piyush-sachdeva) and [@CloudOps Community](https://www.linkedin.com/company/thecloudopscomm)
#40daysofkubernetes #Kubernetes #DaemonSet #Job #CronJob #DevOps #ContainerOrchestration