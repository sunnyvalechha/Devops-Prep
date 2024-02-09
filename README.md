# Devops-inter-prep

**What is difference between Continues Integration and Continues development?** 

**What is Jenkins declaritive pipeline?**

**What are stages and flow of Jenkins CICD pipeline?**

**Difference between Monolithic and Microservices?**

**Explain Kubernetes architecture.**

**What is kubernetes and why it is so popular in container orchestration?**

- because in kubernetes we can managed the life cycle for your deployment in a single environment, there are lot of tools like helm charts and custom operators we can write so we can customize our environment, it can be run in any cloud or without cloud we can run the same image in multiple environments.

**Explain kubernetes and its key components?**

- Pod :

**What is the difference between a Pod and a Deployment in Kubernetes?**

- A pod is smallest deployment unit in kubernetes, a pod can contain one or more than container.
- A deployment on the other hand, manages the deployment and scaling of pod. It ensures that specified number of replicas of a pod must running at any time. It also support the rolling update and rollbacks.

**How does Kubernetes handle storage, and what are Persistent Volumes (PV) and Persistent Volume Claims (PVC)?**

- Persistent volume is a way to define the storage data to the pod. PV is a object in a kubernetes cluster.
- To use Persistent volume it must be requested through Persistent volume clain (PVC). A PVC volume is a request for storage.
- A PVC is used to mount a PV into a pod.
- We can map different classes to different services levels and different backend policies.

**Features of Persistent Volume**.

- Capacity: Generally a PV will specify storage capacity. This is set by set the storage capacity of PV.
- Volume Models: Kubernetes supports 2 volume modes of Persistent volume. A valid value for volume mode can be either file system or block. Filesystem is the default mode.
- Access Modes:
  1. Read Only Many (ROX) - allows being mounted by multiple nodes in read-only mode.
  2. Read Write Once (RWO) - allows being mounted by a single node in read-write mode.
  3. Read Write Many (RWX) - allow multiple nodes to be mounted in read-write mode.
     
