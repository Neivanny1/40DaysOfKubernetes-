# Day 40/40 - Mastering JSONPath and Advanced Kubectl Commands 🚀

## 🎉 Completion Milestone: 40 Days of Kubernetes Learning Challenge
<img src='./assets/40.png'>

The final day of the #40daysofkubernetes challenge focuses on JSONPath queries and advanced kubectl commands, which are essential for querying and manipulating Kubernetes resources efficiently.

## What is JSONPath?

JSONPath is a query language used to extract specific data from JSON objects. Kubernetes resources are represented in JSON format, making JSONPath a powerful tool for customizing kubectl output.

### Basic Syntax:

* $ represents the root of the JSON object.
* . accesses child elements.
* [?(@.field)] applies filters.

## Task Highlights
#### 1. Sorting Running Pods by Creation Timestamp
```
kubectl get pods --field-selector=status.phase=Running \
-o=jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.metadata.creationTimestamp}{"\n"}{end}' \
| sort -k2
```
This command:

* Filters only running pods.
* Outputs pod names and their creation timestamps.
* Sorts the results by the timestamp column.

#### 2. Sorting Nodes by CPU Capacity Using Custom Columns
```
kubectl get nodes -o=custom-columns="NODE:.metadata.name,CPU:.status.capacity.cpu" \
| sort -k2 -n
```
This command:

* Displays nodes with their names and CPU capacity.
* Sorts the output numerically by CPU capacity.

#### 3. Counting Schedulable Nodes (Excluding Tainted)
```
kubectl get nodes --no-headers \
--field-selector=spec.taints[0].effect!=NoSchedule \
-o=custom-columns="NODE:.metadata.name" \
| wc -l > schedulable_nodes_count.txt
```
This command:

* Filters out nodes with NoSchedule taints.
* Counts the remaining schedulable nodes.
* Writes the count to a file named schedulable_nodes_count.txt.

## Key Takeaways

1. JSONPath Mastery: JSONPath allows for precise and customized queries, making resource management more efficient.

2. Advanced Kubectl Queries: Leveraging advanced kubectl commands improves productivity, especially when managing large clusters.

3. Real-World Applications: These skills are invaluable for automating tasks, debugging issues, and acing the CKA exam.

## 📽️ Video Reference

Check out the video below for Day40 👇

[![Day 40/40 - JSONPath Tutorial - Advanced Kubectl Commands](https://img.youtube.com/vi/l9_UDSaiFj4/sddefault.jpg)](https://youtu.be/l9_UDSaiFj4)

## Share Your Learnings

Completing the #40daysofkubernetes challenge has been an enriching experience. Each task reinforced critical Kubernetes concepts, from cluster setup to advanced debugging. Mastering Kubernetes takes consistent practice, and this journey is just the beginning.

How do you leverage JSONPath and advanced kubectl commands in your Kubernetes workflows? Share your tips in the comments!

Tagging: [@Eric mwakazi](https://www.linkedin.com/in/eric-mwakazi), [@PiyushSachdeva](https://www.linkedin.com/in/piyush-sachdeva) and [@CloudOps Community](https://www.linkedin.com/company/thecloudopscomm)

#40daysofkubernetes #KubernetesJSONPath #DevOps
