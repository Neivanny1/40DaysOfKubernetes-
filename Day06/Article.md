# Day 6 of 40 Days of Kubernetes: Setting Up a Single and Multi-Node KIND Cluster for Kubernetes

Today’s task dives into setting up Kubernetes IN Docker (KIND) for both a single-node and multi-node Kubernetes cluster. KIND is a great tool for local development and testing as it creates Kubernetes clusters inside Docker containers. In this article, I’ll walk you through installing and managing a KIND cluster, running on Kubernetes versions 1.29 and 1.30.
Step 1: Installing a Single-Node KIND Cluster (Kubernetes 1.29)
## STEP 1
To start, I installed a single-node Kubernetes cluster using KIND. Here’s a quick rundown of how to do it:
1. Install KIND by following the official KIND documentation.
2. To create a single-node cluster using Kubernetes version 1.29, I ran the following command:
```
kind create cluster --image kindest/node:v1.29.0
```
This simple command spins up a Kubernetes cluster in a Docker container.

3. I used the kubectl get nodes command to verify that the node was up and running:
```
kubectl get nodes
```
## Step 2:
### Deleting the Single-Node Cluster

After verifying the setup, I removed the single-node cluster to move on to the multi-node setup:
```
kind delete cluster
```
This command instantly deletes the cluster and frees up resources on my machine.
## Step 3:
### Installing a Multi-Node KIND Cluster (Kubernetes 1.30)

Next, I created a multi-node KIND cluster with the following configuration:

    1 control plane node
    3 worker nodes
    Kubernetes version 1.30

To create the multi-node cluster, I wrote a kind-config.yaml file with the following content:
```
##conf.yaml

kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
name: cka-cluster2
nodes:
  - role: control-plane
  - role: worker
  - role: worker
  - role: worker

```
I then ran the command:
```
kind create cluster --config kind-config.yaml --image kindest/node:v1.30.0
```
This launched a Kubernetes cluster with multiple nodes running as Docker containers.
## Step 4:
### Installing Kubectl and Managing the Cluster
I made sure to install kubectl, the Kubernetes command-line tool, by following the official docs.

After the KIND cluster was up, I set the current context to the new multi-node cluster:
```
kubectl config use-context kind-cka-cluster2
```
To verify the cluster was set up correctly, I ran:
```
kubectl get nodes
```
This listed all the control plane and worker nodes running inside Docker containers. To cross-check, I also ran:
```
docker ps
```
This confirmed that the nodes were indeed Docker containers, a key feature of KIND.
Key Learnings and Benefits of Using KIND

>>>KIND is perfect for setting up a lightweight local Kubernetes environment without needing a full VM or cloud setup.
Single-node and multi-node configurations can be easily spun up with specific Kubernetes versions, making it ideal for testing.
Docker containers as nodes: KIND uses Docker containers to simulate Kubernetes nodes, keeping everything compact and easy to manage.
>>>
## Final Thoughts

Setting up KIND for Kubernetes is a straightforward process and a great way to practice Kubernetes in a local, resource-efficient environment. It’s an excellent tool for learning, testing, and rapid iteration before scaling to larger environments.

Make sure to check out the official video tutorial and the KIND documentation. I’ve included all the commands and tips I used here, so feel free to try it out!

[![Day 6/40 - Single and Multi-Node KIND Cluster](https://img.youtube.com/vi/RORhczcOrWs/sddefault.jpg)](https://youtu.be/RORhczcOrWs)


Stay tuned for more Kubernetes insights as we continue this 40-day journey!

#40daysofkubernetes
Tagging @PiyushSachdeva and @CloudOps Community.