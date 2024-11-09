# Day 24/40 - Kubernetes RBAC Continued: ClusterRole and ClusterRoleBinding 🌐🔒

<img src='./assets/24.png'>

Today’s focus was on ClusterRoles and ClusterRoleBindings in Kubernetes, which extend permissions beyond individual namespaces to manage resources across the entire cluster. These components are crucial for tasks like managing nodes, PVs, and other cluster-wide resources.

## 🔍 Key Concepts
### Roles and RoleBindings Recap
Roles: Define permissions within a namespace (e.g., get, view, delete Pods).
    RoleBindings: Connect a Role to a specific user or group within a namespace.

### permissions that span across all namespaces. Useful for managing cluster-scoped resources, such as nodes and PVs.

ClusterRoleBindings: Link ClusterRoles to users or groups, enabling them to access cluster-wide resources.

## 🛠️ Key Commands

### List Available Resources:
1. Check all cluster-scoped resources:
```
kubectl api-resources --namespaced=false
```
### Check namespace-scoped resources:
```
kubectl api-resources --namespaced=true
```
### Create a ClusterRole that allows read-only access to nodes:
```
kubectl create clusterrole node-reader --verb=get,list,watch --resource=nodes
```

### Create a ClusterRoleBinding to link the node-reader ClusterRole to a user (e.g., adam):
```
kubectl create clusterrolebinding node-reader-binding --clusterrole=node-reader --user=adam
```
### Check Permissions for the adam user on nodes:
```
kubectl auth can-i get nodes --as adam
```

## 📝 Results and Observations

1. Read-Only Node Access: Once bound to node-reader, the adam user can list and view nodes but cannot modify them.
2. Permissions Scope: Using ClusterRoles and ClusterRoleBindings gives users access to resources beyond individual namespaces, which is essential for cluster-wide operations.

## 🔑 Key Takeaways

1. Roles vs. ClusterRoles: Roles are confined to specific namespaces, whereas ClusterRoles have cluster-wide access.

2. Security: Carefully assigning ClusterRoles ensures that only the necessary users or groups get access to sensitive resources, minimizing the risk of unauthorized access.

3. Use Case for ClusterRoles: Ideal for admin-level or cluster-management tasks where permissions are needed across all namespaces.

## 📽️ Video Reference

For a detailed walkthrough, check out the Day 24 video on Kubernetes ClusterRoles and ClusterRoleBindings:

[![Day Day 23/40 - Kubernetes RBAC Continued - Clusterrole and Clusterrole Binding ](https://img.youtube.com/vi/DswQe7shSa4/sddefault.jpg)](https://youtu.be/DswQe7shSa4)

## 🔗 Share Your Insights

Learning ClusterRoles and ClusterRoleBindings empowers us to set up secure, scalable Kubernetes clusters. Share your thoughts, and let’s connect! Tagging [@Eric mwakazi](https://www.linkedin.com/in/eric-mwakazi), [@PiyushSachdeva](https://www.linkedin.com/in/piyush-sachdeva) and [@CloudOps Community](https://www.linkedin.com/company/thecloudopscomm) to join the discussion.

#40daysofkubernetes #RBAC #ClusterRoles #Kubernetes #DevOps
