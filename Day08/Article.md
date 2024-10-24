For Day 8/40 of the #40daysofkubernetes challenge, I focused on creating and managing Kubernetes ReplicaSets and Deployments. Here’s a breakdown of what I learned and the steps I took:
ReplicaSet:

    Creating a ReplicaSet: I created a new ReplicaSet based on the nginx image with 3 replicas using the following command:

    bash

kubectl create replicaset nginx --image=nginx --replicas=3

Updating the ReplicaSet:

    I updated the number of replicas to 4 by editing the YAML file.
    Then, I scaled it to 6 replicas directly from the command line with:

bash

    kubectl scale replicaset nginx --replicas=6

Deployment:

    Creating a Deployment: I created a Deployment named nginx with 3 replicas using nginx:1.23.0 and applied the label tier=backend to the Deployment, and app=v1 to the Pod template.

    bash

kubectl create deployment nginx --image=nginx:1.23.0 --replicas=3 --labels="tier=backend"

Updating the Deployment: I updated the image to nginx:1.23.4 and ensured the update was rolled out across all replicas.

bash

kubectl set image deployment/nginx nginx=nginx:1.23.4
kubectl rollout status deployment/nginx

Managing the Rollout: After assigning a rollout cause "Pick up patch version", I checked the deployment history and reverted back to the first revision to ensure all replicas reverted to nginx:1.23.0.

bash

    kubectl rollout history deployment/nginx
    kubectl rollout undo deployment/nginx --to-revision=1

Troubleshooting YAML Issues:

I encountered and resolved common YAML errors while deploying new resources and documenting every command I ran during the troubleshooting.
Key Takeaways:

    Kubernetes allows seamless scaling of applications using ReplicaSets and Deployments.
    The power of rollbacks in Deployments is invaluable for ensuring application stability during updates.
    YAML errors are common but easily fixable with proper inspection.

Make sure to follow along for more updates as I continue the #40daysofkubernetes challenge!

🎥 Check out the video for Day 6 here: Watch Now

#Kubernetes #CloudOps #Learning #PiyushSachdeva #CloudOpsCommunity