# Day 19/40 - ConfigMaps and Secrets in Kubernetes 🔐

<img src='./assets/18.png'>

Today's journey in Kubernetes centered on ConfigMaps and Secrets—two essential objects for handling configuration data and sensitive information in a secure, organized way. These resources help in managing configuration and credentials outside of the application code, improving maintainability, security, and flexibility.

Below is an outline of what I learned and implemented.

## 🛠 Task Overview
### 1. ConfigMaps in Kubernetes

> Purpose: ConfigMaps allow you to decouple environment-specific configurations from your container images, reducing the need to bake configuration data into the image.

> Implementation: I created a ConfigMap to store key-value pairs and injected them as environment variables into a pod.
Command:
```
kubectl create cm <configmapname> --from-literal=color=blue --from-literal=color=red
```
YAML Example:
```
apiVersion: v1
data:
  firstname: piyush
  lastname: sachdeva
kind: ConfigMap
metadata:
  name: app-cm

```
### 2. Secrets in Kubernetes
> Purpose: Secrets are designed to store sensitive data, such as passwords or API keys, securely. They ensure confidential information is not exposed within the application’s source code.
Task: Followed Kubernetes documentation to define environment variables using secret data and injected them securely into pods.

## 📘 Key Takeaways on ConfigMaps and Secrets
ConfigMaps:

    Simplifies configuration management by allowing storage of data as key-value pairs outside the manifest.
    ConfigMaps can be reused across multiple pods, ensuring consistency and reducing redundancy.

Secrets:

    Designed to securely manage sensitive data.
    Secrets can be injected as environment variables or mounted as volumes, reducing exposure of sensitive data in plain text.

Practical Uses:

    ConfigMaps and Secrets improve flexibility by enabling updates to configuration or secrets without redeploying the application.

## 📺 Video Reference For a step-by-step walkthrough, check out the Day 19 video on ConfigMaps and Secrets.
[![Day 19/40 - kubernetes configmap and secret](https://img.youtube.com/vi/Q9fHJLSyd7Q/sddefault.jpg)](https://youtu.be/Q9fHJLSyd7Q)

## Sharing

If you’re managing sensitive information or complex configurations in Kubernetes, ConfigMaps and Secrets are game changers! Share your thoughts and experiences using #40daysofkubernetes, and tag [@Eric mwakazi](https://www.linkedin.com/in/eric-mwakazi), [@PiyushSachdeva](https://www.linkedin.com/in/piyush-sachdeva) and [@CloudOps Community](https://www.linkedin.com/company/thecloudopscomm)

#Kubernetes #DevOps #40DaysOfKubernetes #ConfigMaps #Secrets #CloudComputing #Security