# Day 8 of 40 Days of Kubernetes: Deployment with multiple replicas. in Kubernetes ☸️

<img src="./assets/DALL·E 2024-10-24 12.20.33 - A professional LinkedIn cover image for an article about Kubernetes, focusing on ReplicaSets and Deployments. The image should include visual elements.webp">

For Day 8/40 of the #40daysofkubernetes challenge, I focused on creating and managing Kubernetes ReplicaSets and Deployments. Here’s a breakdown of what I learned and the steps I took:

## ReplicaSet
### Creating a ReplicaSet:
I created a new ReplicaSet based on the nginx image with 3 replicas using the following command:
```
kubectl create replicaset nginx --image=nginx --replicas=3
```
### Updating the ReplicaSet
1. I updated the number of replicas to 4 by editing the YAML file.
2. Then, I scaled it to 6 replicas directly from the command line with:
```
kubectl scale replicaset nginx --replicas=6
```
### Deployment
#### Creating a Deployment:
I created a Deployment named nginx with 3 replicas using nginx:1.23.0 and applied the label tier=backend to the Deployment, and app=v1 to the Pod template.
```
kubectl create deployment nginx --image=nginx:1.23.0 --replicas=3 --labels="tier=backend"
```
#### Updating the Deployment:
I updated the image to nginx:1.23.4 and ensured the update was rolled out across all replicas.
```
kubectl set image deployment/nginx nginx=nginx:1.23.4
kubectl rollout status deployment/nginx
```

#### Managing the Rollout:
After assigning a rollout cause "Pick up patch version", I checked the deployment history and reverted back to the first revision to ensure all replicas reverted to nginx:1.23.0.
```
kubectl rollout history deployment/nginx
kubectl rollout undo deployment/nginx --to-revision=1
```
### Troubleshooting YAML Issues:

I encountered and resolved common YAML errors while deploying new resources and documenting every command I ran during the troubleshooting.
## Key Takeaways:
1. Kubernetes allows seamless scaling of applications using ReplicaSets and Deployments.
2. The power of rollbacks in Deployments is invaluable for ensuring application stability during updates.
3. YAML errors are common but easily fixable with proper inspection.

Make sure to follow along for more updates as I continue the #40daysofkubernetes challenge!

🎥 Check out the video for Day 6 here: Watch Now
[![Day 7/40 - Single and Multi-Node KIND Cluster](https://img.youtube.com/vi/oe2zjRb51F0/sddefault.jpg)](https://youtu.be/oe2zjRb51F0)

### References:
#### Cheatsheet for Kubernetes commands: https://kubernetes.io/docs/reference/kubectl/quick-reference/

#### Replicaset: https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/

#### Deployment: https://kubernetes.io/docs/concepts/workloads/controllers/deployment/

#### Replication Controller: https://kubernetes.io/docs/concepts/workloads/controllers/replicationcontroller/

### Share Your Learnings
I encourage you to share your learnings publicly. Feel free to connect and tag me [@Eric mwakazi](https://www.linkedin.com/in/eric-mwakazi), [@PiyushSachdeva](https://www.linkedin.com/in/piyush-sachdeva) and [@CloudOps Community](https://www.linkedin.com/company/thecloudopscomm), and use the hashtag #40daysofkubernetes.
