# Day 10/40 - Kubernetes Namespaces Explained: How to Isolate and Manage Resources Effectively 🛠️

<img src='./assets/10.png'>

Today’s focus was on understanding Kubernetes Namespaces and using them to organize and isolate resources within a Kubernetes cluster. Namespaces offer a powerful way to control access and manage different environments within the same cluster. Here’s what I learned and a summary of today’s tasks.

## 🛠 Task Overview

### Creating Namespaces for Resource Isolation:
Created two namespaces, ns1 and ns2, to test resource isolation in Kubernetes.
### Deploying Applications Across Namespaces:
Created a deployment named deploy-ns1 in ns1 and deploy-ns2 in ns2, each with an nginx pod. After deployment, I retrieved the IP addresses of the pods and verified the connectivity between them.

### Testing Inter-Namespace Connectivity:
Accessed the deploy-ns1 pod to test connectivity with deploy-ns2 by running a curl command to the pod IP in the other namespace. The response confirmed successful pod-to-pod communication across namespaces.

### Scaling and Service Exposure:
Scaled each deployment to three replicas and created services (svc-ns1 and svc-ns2) to expose each deployment.

Verified the service connectivity using curl from one namespace’s pod to the other’s service IP, which worked as expected.

## Understanding FQDN for Cross-Namespace Service Access:
When using the service name directly, the pods were unable to resolve it.

Using the Fully Qualified Domain Name (FQDN) in the format service-name.namespace.svc.cluster.local successfully resolved the service names across namespaces.

### Cleaning Up:
Deleted both namespaces, which in turn removed all resources associated with them.

## 📘 Key Takeaways on Kubernetes Namespaces

### Namespace Benefits:
#### Isolation of Resources:
Namespaces provide isolation, preventing accidental modification or deletion of resources in unrelated environments.
#### Organizational Clarity:
Namespaces allow resources to be segmented by project, environment (e.g., dev, test, prod), or resource type.
#### Namespace DNS Conventions:
Kubernetes resolves resources within a namespace by their names. For cross-namespace access, using the FQDN format (e.g., service-name.namespace.svc.cluster.local) allows inter-namespace connectivity.

### Practical Use of Namespaces

Namespaces are especially valuable in multi-tenant environments, as well as in projects where different application components need to be isolated for enhanced management, security, and resource allocation.
## 📺 Video Reference

For a full walkthrough, watch the Day 10 video on Kubernetes Namespaces: 

[![Day10/40 - Kubernetes Namespace Explained - CKA Full Course 2024](https://img.youtube.com/vi/yVLXIydlU_0/sddefault.jpg)](https://youtu.be/yVLXIydlU_0)

## SHARING
Feel free to share your thoughts, insights, or questions about using namespaces in Kubernetes!

Tags:

[@Eric mwakazi](https://www.linkedin.com/in/eric-mwakazi), [@PiyushSachdeva](https://www.linkedin.com/in/piyush-sachdeva) and [@CloudOps Community](https://www.linkedin.com/company/thecloudopscomm)

#40daysofkubernetes #Kubernetes #Namespaces #DevOps #ContainerManagement #CloudComputing #Microservices #FQDN