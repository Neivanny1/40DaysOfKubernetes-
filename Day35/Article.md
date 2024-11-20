Day 35/40 - Kubernetes ETCD Backup and Restore Explained🌐📥

<img src='./assets/35.png'>

Backing up and restoring ETCD is critical for maintaining the integrity and availability of your Kubernetes cluster. ETCD stores all the cluster’s state data, so mastering its backup and restore process is essential for disaster recovery.
What Is ETCD?

ETCD is a distributed key-value store used by Kubernetes to manage cluster data. It stores all the information about the cluster, including nodes, deployments, and configurations.

    Why Backup ETCD?
    Backups help safeguard your cluster state in case of data corruption, accidental deletion, or cluster failure.

Step-by-Step ETCD Backup and Restore Process
Preparation

    Log in to Your Control Plane Node
    Ensure you have access to the control plane node where ETCD runs.

    Check Node Health
    Verify that all nodes are in a Ready state:

kubectl get nodes

Find the ETCD Version
Check the version of ETCD installed:

etcdctl version

Deploy a Sample Application
Create an Nginx deployment with two pods:

kubectl create deployment nginx --image=nginx
kubectl scale deployment nginx --replicas=2

Verify the deployment:

    kubectl get pods

Backing Up ETCD

    Set Up Environment Variables
    Set ETCDCTL_API to version 3:

export ETCDCTL_API=3

Identify ETCD Endpoint and Certificates
Find the ETCD endpoint and certificates needed for communication:

ETCD_ENDPOINTS=https://127.0.0.1:2379
CERT_DIR=/etc/kubernetes/pki/etcd

Take a Snapshot Backup
Run the following command to create a snapshot:

etcdctl --endpoints=$ETCD_ENDPOINTS \
        --cacert=$CERT_DIR/ca.crt \
        --cert=$CERT_DIR/peer.crt \
        --key=$CERT_DIR/peer.key \
        snapshot save /opt/etcd-snapshot.db

Confirm the backup:

    ls -l /opt/etcd-snapshot.db

Restore ETCD from Backup

    Delete the Deployment
    Simulate data loss by deleting the Nginx deployment:

kubectl delete deployment nginx

Restore the Snapshot
Restore the backup to a new directory:

etcdctl snapshot restore /opt/etcd-snapshot.db \
        --data-dir /var/lib/etcd-from-backup

Update ETCD to Point to the Restored Data
Modify the ETCD configuration file or update the pod manifest to use /var/lib/etcd-from-backup as the data directory.

Restart ETCD
Restart the ETCD pod or service:

sudo systemctl restart etcd

Verify the Deployment
Check that the restored Nginx deployment is available:

    kubectl get deploy

Key Learnings and Reflections

    Critical Data: ETCD contains all cluster configuration data; protecting it ensures business continuity.
    Proactive Backup: Regularly take snapshots to prepare for unexpected issues.
    Restoration Process: The ETCD restore process demonstrates how Kubernetes supports disaster recovery while maintaining high availability.

## 📽️ Video Reference

Check out the video below for Day35 👇

[![Day 35/40 - Kubernetes ETCD Backup And Restore Explained](https://img.youtube.com/vi/R2wuFCYgnm4/sddefault.jpg)](https://youtu.be/R2wuFCYgnm4)

Share Your Learnings

Sharing is learning! Here’s how I backed up and restored my Kubernetes cluster. What’s your approach to cluster disaster recovery?

Tagging: [@Eric mwakazi](https://www.linkedin.com/in/eric-mwakazi), [@PiyushSachdeva](https://www.linkedin.com/in/piyush-sachdeva) and [@CloudOps Community](https://www.linkedin.com/company/thecloudopscomm) 
Hashtags: #40daysofkubernetes #KubernetesETCD #DevOps