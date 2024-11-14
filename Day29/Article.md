# Day 29/40 - Kubernetes Volumes Simplified | Persistent Volume, Persistent Volume Claim & Storage Class 📂💾

<img src='./assets/29.png'>

Today’s Goal: Deep dive into Kubernetes volumes, focusing on Persistent Volumes (PVs), Persistent Volume Claims (PVCs), and Storage Classes. These components are key to managing storage in Kubernetes and enabling stateful applications with persistent data.

## Overview: Kubernetes Persistent Storage

In Kubernetes, volumes support persistent storage by detaching data from pod lifecycles. Unlike traditional storage, persistent volumes ensure that data is accessible and retained even if a pod is deleted or redeployed. Today, we’ll walk through examples of setting up Persistent Volumes, creating Persistent Volume Claims, and applying Storage Classes.

## Key Concepts in Kubernetes Storage

1. Persistent Volume (PV): A storage unit provisioned by an administrator, independent of any particular pod. It can be based on local storage or cloud provider storage and supports multiple access modes.

2. Persistent Volume Claim (PVC): A request for storage by a user, specifying attributes like size and access mode. When matched, the PVC binds to an available PV.

3. Storage Class: Defines the types of storage available within the Kubernetes cluster, enabling dynamic provisioning and customization of storage resources.

## Implementing Persistent Storage in Kubernetes

Let’s work through a practical example to set up a persistent volume, persistent volume claim, and bind it to a pod.
### Step 1: Create a PersistentVolume (PV)

Using ReadWriteMany access mode with a 512Mi storage capacity, here’s the configuration for a persistent volume:
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-demo
  labels:
    type: local
spec:
  storageClassName: ""
  capacity:
    storage: 512Mi
  accessModes:
    - ReadWriteMany
  hostPath:
    path: "/data/config"
```
### Step 2: Set Up a PersistentVolumeClaim (PVC)

The following example configures a PVC that requests 256Mi of storage:
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-demo
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 256Mi
  storageClassName: ""
```
Run this YAML file to create the PVC, which will bind automatically if there’s a matching PV.
### Step 3: Deploy a Pod that Mounts the PersistentVolumeClaim

Create a pod named app, mounting the pvc-demo volume at /var/app/config:
```
apiVersion: v1
kind: Pod
metadata:
  name: app
spec:
  volumes:
    - name: app-storage
      persistentVolumeClaim:
        claimName: pvc-demo
  containers:
    - name: nginx-container
      image: nginx:latest
      volumeMounts:
        - mountPath: "/var/app/config"
          name: app-storage
```
### Step 4: Verify Persistence

#### Access the Pod:
```
kubectl exec -it app -- /bin/sh
```
#### Create a Test File:
```
echo "Hello, Kubernetes Storage!" > /var/app/config/test-file.txt
```
This demonstrates the effectiveness of persistent storage by ensuring that data remains accessible even when the pod restarts.

## Key Takeaways

1. Persistent Volumes (PV) & Claims (PVC): PVs provide persistent storage across pods, while PVCs allow users to claim and use this storage based on specific requirements.
2. Storage Class Customization: Enables fine-tuning of storage resources in Kubernetes, essential for stateful applications needing scalable storage solutions.
3. Real-world Use Case: Using PVs and PVCs in Kubernetes ensures data persists across pod lifecycles, a crucial capability for applications with permanent storage needs.

## 📽️ Video Reference
For added context, check out the video on Kubernetes Persistent Volumes below.
Sharing Progress
[![Day 29/40 Kubernetes Volume Simplified | Persistent Volume, Persistent Volume Claim & Storage Class ](https://img.youtube.com/vi/2NzYX8_lX_0/sddefault.jpg)](https://youtu.be/2NzYX8_lX_0)

## Sharing Progres
I’ve documented today’s learnings and will be sharing on LinkedIn. Tagging [@Eric mwakazi](https://www.linkedin.com/in/eric-mwakazi), [@PiyushSachdeva](https://www.linkedin.com/in/piyush-sachdeva) and [@CloudOps Community](https://www.linkedin.com/company/thecloudopscomm) with the hashtag #40daysofkubernetes.