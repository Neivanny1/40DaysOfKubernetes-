# Day 5 of 40 Days of Kubernetes: Kubernetes Architecture and Control Plane Components 🌐☸️
<img src='./assets/DALL·E 2024-10-21 17.52.20 - A Kubernetes architecture diagram showing the control plane and worker nodes. The control plane should include components such as the API Server, etcd.webp'>

For Day 5 of the #40DaysOfKubernetes challenge, I explored the architecture of Kubernetes, created an architecture diagram, and learned about the control plane components that manage the cluster.

## Kubernetes Architecture Overview 🖼️

Kubernetes follows a master-worker architecture, where the control plane manages worker nodes. The worker nodes host Pods, which are the smallest deployable units in Kubernetes that run your containers.

<img src='./assets/Screenshot at 2024-10-21 20-46-00.png'>

### Here’s a brief overview of the Control Plane components:

1. API Server: The frontend of the Kubernetes control plane. It receives all requests (like kubectl commands) and forwards them to the right components.
2. etcd: The key-value store that acts as the brain of Kubernetes, storing the cluster's state and configurations.
3. Controller Manager: Ensures the actual state of the cluster matches the desired state (like ensuring a Pod restarts if it crashes).
4. Scheduler: Assigns newly created Pods to nodes based on resource requirements and availability.
5. Kubelet: The agent running on each worker node that ensures containers are running in a Pod.
6. Kube Proxy: Manages network communication within the cluster, ensuring proper routing of traffic between Pods and services.

### End-to-End Flow of a kubectl Command

When you run a command like kubectl apply -f deployment.yaml, this is what happens:

<img src='./assets/DALL·E 2024-10-21 17.50.42 - A diagram depicting the end-to-end flow of a &apos;kubectl apply&apos; command in Kubernetes. The flow should start with the user executing &apos;kubectl&apos; from the c.webp'>

kubectl sends the request to the API Server.
The API Server authenticates and validates the request, then stores it in etcd.
The Scheduler checks for available nodes and assigns the Pod to the most suitable node.
Kubelet on the chosen node pulls the container image and starts the Pod.
The Controller Manager monitors the system to ensure the Pod remains in the desired state.

## Pods and Containers 🛠️

In Kubernetes, a Pod is the smallest unit of deployment. Each Pod encapsulates one or more containers, which share the same network and storage. While Docker is the most common container runtime, Kubernetes can run containers using different runtimes.
### Pod Characteristics:

1. Pods are ephemeral: Once they are created, they can be terminated or recreated if they fail.

2. Shared Networking: All containers in a Pod share the same IP address, allowing them to communicate easily.
3. Volumes: Pods can include shared storage volumes that persist across container restarts.

### Key Takeaways
1. The Kubernetes control plane orchestrates everything—from scheduling Pods to managing container networking.
2. Kubernetes abstracts away much of the complexity involved in managing large-scale containerized applications.
3. Pods are the core unit of deployment, but Kubernetes takes care of load balancing, scheduling, and self-healing, making it much easier to manage applications.


## Video Lesson:

[![Day 5/40 - What is Kubernetes - Kubernetes Architecture Explained](https://img.youtube.com/vi/SGGkUCctL4I/sddefault.jpg)](https://youtu.be/SGGkUCctL4I)

### References:
#### Kubernetes Documentation: https://kubernetes.io/docs/concepts/overview/
#### Docker Best Practices: https://docs.docker.com/build/building/best-practices/

Thank you [@PiyushSachdeva](https://www.linkedin.com/in/piyush-sachdeva) and [@CloudOps Community](https://www.linkedin.com/company/thecloudopscomm)

Stay tuned for more learnings on Kubernetes orchestration and deployment in the upcoming tasks!

#Kubernetes #CloudNative #DevOps #40DaysOfKubernetes #CKA