# Day 31/40 - Understanding CoreDNS in Kubernetes 🧭🔍

<img src='./assets/31.png'>

Today’s focus was on CoreDNS, the default DNS server and service discovery mechanism in Kubernetes. CoreDNS is a critical component for managing cluster-wide DNS, enabling seamless communication between services.

## 🤔 What is CoreDNS?

CoreDNS is a flexible and extensible DNS server designed specifically for Kubernetes. It acts as the default cluster DNS, resolving service names to their corresponding IPs within a Kubernetes environment. Beyond simple DNS queries, CoreDNS supports advanced features like service discovery, load balancing, and custom DNS plugins.

## 📋 Key Steps for Exploring CoreDNS

### 1. Check the CoreDNS Deployment:
To verify that CoreDNS is running in your cluster:
```
kubectl get pods -n kube-system
````
Look for coredns pods in the output.

### 2. Inspect the CoreDNS ConfigMap:
CoreDNS configuration is managed via a ConfigMap. Retrieve it using:
```
kubectl -n kube-system get configmap coredns -o yaml
```
Example of CoreDNS configuration:
```
.:53 {
    errors
    health
    ready
    kubernetes cluster.local in-addr.arpa ip6.arpa {
        pods insecure
        fallthrough in-addr.arpa ip6.arpa
    }
    prometheus :9153
    forward . /etc/resolv.conf
    cache 30
    loop
    reload
    loadbalance
}
```
### 3. Modify CoreDNS ConfigMap:
To enable additional features or debugging, you can edit the ConfigMap:
```
kubectl -n kube-system edit configmap coredns
```
### 4. Test CoreDNS Resolution:
To test DNS resolution from within a pod:
```
kubectl run -it --rm debug --image=busybox --restart=Never -- nslookup <service-name>
```
Replace <service-name> with the name of the service you want to resolve.

## 🔍 Key Observations

1. Service Discovery: CoreDNS seamlessly maps service names to cluster IPs, enabling communication between pods.
2. Custom Plugins: CoreDNS supports plugins for extended functionality like metrics, debugging, and more.
3. Configurable Behavior: By modifying the ConfigMap, you can customize CoreDNS behavior to fit specific requirements.

## 📝 Key Takeaways

1. CoreDNS is essential for Kubernetes networking: It handles DNS-based service discovery and routing.
2. Flexibility and Extensibility: With its plugin architecture, CoreDNS can adapt to varied use cases.
3. Centralized Management: Using ConfigMaps, administrators can manage CoreDNS configurations cluster-wide.

## 📽️ Video Reference

For an in-depth guide, check out the video on CoreDNS:

[![Day 31/40 - Understanding CoreDNS In Kubernetes ](https://img.youtube.com/vi/VcWpZoRAQXE/sddefault.jpg)](https://youtu.be/VcWpZoRAQXE)


## 🔗 Share Your Insights

Today’s learnings shed light on how CoreDNS ensures smooth communication in Kubernetes clusters. Have you worked with CoreDNS before? What’s your biggest takeaway from today’s post?

Tagging [@Eric mwakazi](https://www.linkedin.com/in/eric-mwakazi), [@PiyushSachdeva](https://www.linkedin.com/in/piyush-sachdeva) and [@CloudOps Community](https://www.linkedin.com/company/thecloudopscomm)to continue the discussion!

#40daysofkubernetes #CoreDNS #Kubernetes #DevOps