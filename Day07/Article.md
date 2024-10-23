# Day 6 of 40 Days of Kubernetes: Creating, Modifying, and Troubleshooting Pods in Kubernetes ☸️
<img src='./assets/DALL·E 2024-10-23 16.07.13 - A professional LinkedIn cover photo for a blog post about Kubernetes pod creation and troubleshooting. The design should feature a modern, clean tech -1.webp'>

Today’s focus was on learning how to create and modify pods in Kubernetes using both imperative commands and declarative YAML files, along with troubleshooting pod issues. Below is a summary of what I accomplished, along with the steps and insights gained along the way.

## 📽️ Video Lesson: Kubernetes Pod Creation and Troubleshooting
### You can check out the detailed video lesson for Day 7 here:

[![Day 6/40 - Single and Multi-Node KIND Cluster](https://img.youtube.com/vi/_f9ql2Y5Xcc/sddefault.jpg)](https://youtu.be/_f9ql2Y5Xcc)

## Creating, Modifying, and Troubleshooting Pods in Kubernetes
### Task 1: Creating a Pod Imperatively

The first task was to create a pod using the imperative command with nginx as the container image. Here's the command I used:
```
kubectl run nginx --image=nginx
```
This command creates a pod named nginx with the official Nginx image from Docker Hub.

### Learnings:
1. Using kubectl run is an easy and quick way to deploy a pod without writing YAML.
2. The --image flag specifies the container image, and by default, Kubernetes pulls the image from Docker Hub if no registry is specified.

### Task 2: Converting Pod to YAML and Modifying It
Next, I converted the imperatively created pod into a YAML manifest file and modified it:
#### Exporting the YAML:
```
kubectl get pod nginx -o yaml > nginx.yaml
```

Modifying the Pod Name: I opened the nginx.yaml file and updated the pod name to nginx-new:
```
#nginx.yaml

apiVersion: v1
kind: Pod
metadata:
  name: nginx-new
spec:
  containers:
  - name: nginx
    image: nginx
```
#### Creating the Pod Using YAML:
```
kubectl apply -f nginx.yaml
```
### Learnings:
1. The kubectl get pod command is useful to export a live pod's configuration into a YAML file.
2. Applying YAML files provides more flexibility and control over pod configurations compared to imperative commands.

### Task 3: Troubleshooting Pod Creation
In this task, I was asked to apply a YAML configuration for a Redis pod with errors and fix it.
Here's the original YAML file with the errors:
```
apiVersion: v1
kind: Pod
metadata:
  labels:
    app: test
  name: redis
spec:
  containers:
  - image: rediss
    name: redis
```

When I applied this YAML using:
```
kubectl apply -f redis.yaml
```
I encountered the following error message:
>>Failed to pull image "rediss": rpc error: code = Unknown desc = Error response from daemon: pull access denied for rediss, repository does not exist or may require 'docker login'

### 🔧 Fixing the Error:

The issue was that the image name rediss was incorrect. The correct image name is redis. Here’s how I fixed it:
Updated YAML file:
```
apiVersion: v1
kind: Pod
metadata:
  labels:
    app: test
  name: redis
spec:
  containers:
  - image: redis
    name: redis
```
Re-applying the YAML:
```
kubectl apply -f redis.yaml
```
Verifying the Pod:
```
kubectl get pods
```
### Learnings:
1. Image names must be precise, and Kubernetes will attempt to pull the image from the default container registry.
2. The kubectl get pods command is essential for verifying that the pod is in the Running state after deployment.

## Key Takeaways
1. Imperative vs Declarative: The imperative way (kubectl run) is quicker for one-off tasks, while the declarative approach (YAML) is more scalable and maintainable for production use.
2. Troubleshooting Pods: Image pulling errors are common and usually caused by incorrect image names, missing tags, or misconfigured registry credentials.
3. kubectl apply: Using kubectl apply -f is a robust way to deploy complex Kubernetes configurations, as it allows you to track changes in your YAML files.

>>For more best practices on Kubernetes pod management, check out the video embedded above!
References:
Kubernetes official documentation: https://kubernetes.io/docs/home/
Docker Hub: Nginx Image:https://hub.docker.com/_/nginx/

### Share Your Learnings

I encourage you to share your learnings publicly. Feel free to connect and tag me [@Eric mwakazi](https://www.linkedin.com/in/mwakazi-eric), [@PiyushSachdeva](https://www.linkedin.com/in/piyush-sachdeva) and [@CloudOps Community](https://www.linkedin.com/company/thecloudopscomm), and use the hashtag #40daysofkubernetes.