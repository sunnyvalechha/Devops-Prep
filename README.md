# Devops-inter-prep

**What is difference between Continues Integration and Continues development?** 

**What is Jenkins declaritive pipeline?**

**What are stages and flow of Jenkins CICD pipeline?**
- Dev
- Stage
- Prod

  * So the code will deploy to the target platform that is kubernetes with Continues Integration and Continues Delivery approach.
  * Let's say there is a user who want to make change in feature branch or any branch he is assign, in his version control system (GitHub).
  * There is a web hook which triggers the jenkins pipeline.
  * First thing which happen in the pipeline is continues Integration where different stages are there.

      * Code checkout stage: If we are using the java application so we will checkout the java code.
      * Building and Unit testing: We can use maven, to run the application we can trigger the maven targets, once this is successful we will move to the code scanning stage.
      * Code Scanning: We will verify if the code has any static code or any duplicate code, syntax issues. This code analysis can be done through Sonar Cube. After this is successful we will move to the Image build creation.
      * Image build: Container Images we can use docker or podman. Once the container image is created we will scan the image which is created, so for image scanning we have different type of tools like trivy. If this is also working fine we will move to the final stage.
      * Image Push: We will push the Image to the image registry. For this we are using docker hub.
      * Once we have new Image Ex: testimage:v2, we will update the image in kubernetes manifest.
      * As a good practise will should keep our manifest in different repository from source code repository

    ![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/5272cead-ed27-43c0-a82a-1b402f197a47)

* After that the code should move from feature branch to Pre-prod and Production environment.

  ![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/d1ac12b3-9288-4ff8-a751-98fec0ab61d8)

In an organization 3 branch will be there at any point.
1. Feature branch, might be 0, 1 or 2 depends if there any new changes or bug need to enhance.
2. Main branch always be 1
3. Release branch can be carry multiple releases, customer can choose which release version they like to choose.

**Another branch in an organization**

Hotfix Branch: Suppose there might a critical bug in the latest release of an application version. So from that specific version which has a bug, we will create a Hotfix branch, we will fix the code in Hotfix branch
and then we will merge the changes from Feature, Main and Release Branch.

**Promote application from Dev env to Production env**






    

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
 

 ===========================================================================================

 **ImagePullBack Error**

  kubectl create deployment nginx-deploy --image=nginx 

  kubectl get pod -w

  kubectl describe pod nginx-deploy..

Till above everything was fine, we have make error as image does not exit

  kubectl edit deployment nginx-deploy

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/dc16f29b-2f71-4266-95d7-c15b24d33f26)

  kubectl get pods -w 

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/6f45b815-6a33-4507-a671-1c87be22b302)



 
     
