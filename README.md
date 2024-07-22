# Monitoring with Grafana / Prometheus / Thanos

What are challenges with Prometheus? 

# Blue and Green Deployments
Ans: 

# Git

Git Fetch and Git Merge?
* Git Fetch command download the latest changes from the remote repository to your local repository. It does not merge the changes into your current branch. Git pull is a alternative or for Git Fetch.
* To merge the changes we need to run git merge 

Head in Git?
* Head refers to the currently checked-out branch's latest commit. However, in a detached HEAD state, the HEAD does not point to any branch but instead point to a specific commit or the remote repository.

* What is git conflict and why does it occur?
  A Git conflict occurs when you try to merge two branches that have conflicting changes. This can happen when two people are working on the same file at the same time, or when you merge a branch that has been updated since you last merged it.
Git will try to automatically resolve the conflict, but sometimes it can't. When this happens, you'll need to manually resolve the conflict.
To resolve a conflict, you'll need to open the conflicted file and decide which changes you want to keep. You can use a vim text editor to do this.

* What is Git Stash?
  Git stash is a command that saves your uncommitted changes to a temporary stack, so you can switch branches or work on something else without losing your changes. When you're ready to come back to your changes, you can apply the stash and they'll be restored to your working directory.

* What is diffrence between Git and GitHub?
   Git is a distributed version control system for tracking changes in source code during software development.
  GitHub is a web-based Git repository hosting service.

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/b21fc9eb-110e-45ef-bbf7-97a6b75f4fde)

* What is Git Rebase ?
  Rebasing is the process of moving or combining a sequence of commits to a new base commit.

* How to recover deleted branch after push to central repository?
  Using the reflog:
The reflog is a local log of all changes made to the repository, including deleted branches. To recover a deleted branch using the reflog, you can use the following command:

   git reflog
  


# AWS
1. difference in aws auto scaling vs ec2 auto scaling
2. difference in launch template vs launch configuration
3. who is publisher and who is consumer (sqs)
4. cloudfront - uses and need
   Cloud Front is a caching service or a content delivery network where response of the request are cached at a location to reduce the latency.

* Regional Egde cache in Cloud Front.
A regional edge cache in Amazon CloudFront is a location that's deployed globally, close to viewers. They're located between the origin server and the global edge locations (PoPs). 

* Geo Targeting in Cloud Front?
  Geo-targeting in Amazon CloudFront is a feature that allows businesses to show personalized content to their audience based on their geographic location.

  
   
6. when to choose s3 and when to cloudfront
7. Iam roles vs policy
8. aws lambda - use case
9. lambda edge
10. vertical scaling in lambda
--------------------------------
# Ansible
1. Pull and push mechanism
2. day to day task in ansible
3. roles vs playbook
4. playbook vs adhoc commands
5. tags in ansible
6. cowsay in ansible
7. how to access variable in ansible 
8. ansible facts 
9. core, builtIn and extra module
10. maintaining plugins in ansible
11. type of ansible inventory and dynamic inventory (static / dynamic)
12. idempotency

# Docker
What is side car container and when to use one?

**Dockerfile**

FROM ubuntu / Centos / tomcat / golang                 # Represent the base Image. This command executes first when we start building the Image.

VOLUME ["/newdirectory"]                               # Attach a volume inside the container, and with this volume we can attach a local directory called volume mount.

WORKDIR /app                                           # Once the source code build, will store in this directory

COPY <source> <destination>                            # Copy the dependencies from local system to image

RUN apt-get update && pip install requirement.txt      # Execute commands while creating image

ENTRYPOINT ["python3"]                                 # When we start the container the script or command mentioned here is executed (Cannot over write)

CMD ["manage.py", "runserver", "0.0.0.0:8000"]         # Start the process inside the container (Can be over write, means if port 8000 is occupied already we can change but if would have mentiond in ENTRYPOINT we cannot change)



**Multi-stage builds**

Practical:

* Use ubuntu Ec2 instance.
* Install docker
* Install go lang: sudo apt  install golang-go
* clone repo https://github.com/iam-veeramalla/Docker-Zero-to-Hero.git
* cd /home/ubuntu/Docker-Zero-to-Hero/examples/golang-multi-stage-docker-build
* Run calculator app: go run calculator.go

![image](https://github.com/user-attachments/assets/2f717c15-41d9-4f01-ba8b-32e71396cd5d)

Containerize this go app, Without multi-stage

vim dockerfile-without-multistage/Dockerfile

cd /home/ubuntu/Docker-Zero-to-Hero/examples/golang-multi-stage-docker-build/dockerfile-without-multistage

    docker build -t calculator .

    sudo docker images      # Image size is 650 MB

Note: For the basic calculator app we don't require so heavy image

Now use the multi-stage docker build image using Distroless images called SCRATCH

Build the docker image present at /home/ubuntu/Docker-Zero-to-Hero/examples/golang-multi-stage-docker-build

    sudo docker build -t simple-cal-multi .

![image](https://github.com/user-attachments/assets/26319b06-90ab-43a9-9976-d9a53ace38bf)









# Kubernetes

What is the Port range of Service Node-Port? 

30,000 to 32,767

**How to Secure Kubernetes Cluster?**

* Secured sensitive information on Kubernetes cluster

1. Secure your API server
2. Very good with RBAC
3. Cluster network policies are very well defined
4. Information (Data) are encrypted at REST in ETCD
5. Use Secure container Images
6. Cluster Monitoring
7. Frequent Upgrades

Secure your API server - When we run any command let's say 'kubectl get pods' the request first go to API server then API server validate with scheduler, but API server is first point of contact. So the suppose the cluster API server is not secure then the cluster itself can be compromised. So as a DevSecOps engineer we have to secure the API server.

How we will do that? >> /etc/kubernetes/manifest/kube-apiserserver.yaml
* In kubernetes every resource is a pod and API server should also have a pod / pod file. So this kube-api server has a yaml file we have to put TLS certs in the yaml file.
* Then secure this yaml file consist TLS certificates using RBAC


**Encrypting Secrets in etcd (Kubernetes Security)**
    
    kubectl get secret

    kubectl create secret generic new-secret-1 --from-literal=somekey=somevalue

    k describe secret new-secret-1

![image](https://github.com/sunnyvalechha/Devops-Prep/assets/59471885/be4cb6be-6203-4b21-9cee-0e72d057884e)

Note: Anyone who have bad intension and have knowledge of K8 can decode the secret we can see in above image. This text is Encoded not Encrypted. Encoded with base64.

How to see the value of somekey?  >> 

    kubectl get secret -o yaml
    
    kubectl get secret -o yaml > secret.yaml

![image](https://github.com/sunnyvalechha/Devops-Prep/assets/59471885/98b26fb1-d06c-496c-a107-5c29d9798a00)


    echo c29tZXZhbHVl | base64 --decode

![image](https://github.com/sunnyvalechha/Devops-Prep/assets/59471885/d4f0dda5-b873-4871-8502-41676f3233bc)

Note: So this can be seen very easily, even in ETCD it is stored in plain text, check out below

    k get pods -n kube-system

![image](https://github.com/sunnyvalechha/Devops-Prep/assets/59471885/9bc22a6c-0ed5-42f7-857d-1171567c2b16)

Get the certificates first, because to access the ETCD pod we need this authentication

    grep etcd /etc/kubernetes/manifests/kube-apiserver.yaml

    - --etcd-cafile=/etc/kubernetes/pki/etcd/ca.crt
    - --etcd-certfile=/etc/kubernetes/pki/apiserver-etcd-client.crt
    - --etcd-keyfile=/etc/kubernetes/pki/apiserver-etcd-client.key
    - --etcd-servers=https://127.0.0.1:2379

    controlplane $ kubectl -n kube-system exec -it etcd-controlplane -- sh -c \
    > "ETCDCTL_API=3 ETCDCTL_CACERT=/etc/kubernetes/pki/etcd/ca.crt \
    > ETCDCTL_CERT=/etc/kubernetes/pki/etcd/server.crt \
    > ETCDCTL_KEY=/etc/kubernetes/pki/etcd/server.key \
    > etcdctl --endpoints=https://127.0.0.1:2379 get /registry/secrets/default/new-secret-1"

 ![image](https://github.com/sunnyvalechha/Devops-Prep/assets/59471885/c1f78158-6985-427f-b5aa-9a2b0fa583c7)

 Below command is to generate a random encrpted code
 
    head -c 32 /dev/random | base64

    vim encryption.yaml

 ![image](https://github.com/sunnyvalechha/Devops-Prep/assets/59471885/83f0e174-e24f-4c52-9816-2b870cd84bca)

 Code copy from k8 doc: https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/

 We are telling K8 to use this yaml file so moving file into pki folder but here main file is /etc/kubernetes/manifests/kube-apiserver.yaml

    cp encryption.yaml /etc/kubernetes/pki/

Open the file and add the path of "encryption.yaml" file at last and save, exit. 

    vim /etc/kubernetes/manifests/kube-apiserver.yaml

    - --encrption-provider-config=/etc/kubernetes/pki/encryption.yaml
    
![image](https://github.com/sunnyvalechha/Devops-Prep/assets/59471885/c300a1ac-c140-4578-a22c-d8efafccd8b4)

So if we run the same command to see the secret in ETCD, the text will encrypted BUT if we run "echo c29tZXZhbHVl | base64 --decode" the text is still exposed.

**Enforce automated k8s cluster security using kyverno generator and ArgoCD**

Kyverno is a policy engine for Kubernetes that helps platform engineering teams manage security, compliance, and governance. It runs as a dynamic admission controller in a Kubernetes cluster, receiving HTTP callbacks from the Kubernetes API server and applying policies to enforce admission policies or reject requests. 




 **kubectl apply vs kubectl create**
 
   * When running "kubectl create" command it calls the API server, API server then check if the same name available or not (webserver), if not it makes the entry in ETCD then ETCD instruct to the scheduler then response goes back to API and then kubelet create a pod on worker node.
  
   * If we have to add an parameter of labels in same configuration again we run create command again same process repeats but this time we encouter an error called "Pod already exist"
 
   * On the other side "kubectl apply" makes the changes also save the last-applied-configuration time-stamp under annotations and this does not interact with API to make changes instead directly inract with ETCD to update resources this compare Local configuration (yaml file) with Live configuration (kubectl get pod <pod-name> -o yaml). If there is any new changes found it will apply.

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/a806184d-d29a-44a8-b7cb-31ecfa0e323c)

   * apply --> used in production
   * create --> do not used in prod environment
  
**Manually Schedule a Pod**

To check scheduler running or not, scheduler ran on kube-system namespace

  kubectl get pods -n kube-system

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/f49631fa-c3f0-43c5-a8cb-e9cbc8d80d5c)

Scheduler running as pod so first we have to stop the scheduler so that it can schedule pod automatically

  mv /etc/kubernetes/manifests/kube-scheduler.yaml /etc/kubernetes/

So if we run any pod it will go into Pending state because scheduler not present

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/a12cdb30-00a7-437d-8efe-812bd075543e)

Now we will create a manifest and edit our node manually

   kubectl run web2 --image=nginx --dry-run=client -o yaml > web2.yaml

   cat web2.yaml

 ![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/cd5ab15b-5df4-4881-89fa-a238f9562030)

 




   

  
- Kubernetes Pause containers ? - done on k8 full docs
- How 2 containers are running in a single pod having single IP? 
- How do you handle kubernetes security? 
- How do you handle kubernetes secretes?
- What is Init containers and why do we need it ?
- Difference btw voluntary and Invouluntary distruption?
- What is Pod distruption budget ?
- What is Ingress controller ?
- What is Pod Security Policy ?



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

**ImagePullBackOff / ErrImagePull / Invalid Image Name Error**

Two scenerios can be there:
1. Image is not present in a repository like Docker Hub
   Image name is written wrong mistakenly

2. Image is Private and you don't have access to the registry (Permission Denied).

Practical:-

  kubectl create deployment nginx-deploy --image=nginx 

  kubectl get pod -w

  kubectl describe pod nginx-deploy..

Till above everything was fine, we have make error as image does not exit

  kubectl edit deployment nginx-deploy

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/dc16f29b-2f71-4266-95d7-c15b24d33f26)

  kubectl get pods -w 

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/6f45b815-6a33-4507-a671-1c87be22b302)


**Resource Quota Namespace**

kubectl create namespace payments

vim qouta.yml

    apiVersion: v1
    kind: ResourceQuota
    metadata:
      name: mem-cpu-demo
    spec:
    hard:
      requests.cpu: "1"
      requests.memory: 1Gi
      limits.cpu: "2"
      limits.memory: 2Gi

 kubectl apply -f quota.yml -n payments

 kubectl describe ns payments 

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/f8d8b00a-89a3-4352-9654-711fec273f7e)

  kubectl create deploy ngix-dep --image=nginx -n payments

  kubectl get deploy -n payments

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/decd594d-9f2d-44a5-98c7-1893ef7f5cd6)

In above, deployment is created but no pod in ready state, hence nothing found in get pods command 

  kubectl describe deploy nginx-dep -n payments

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/c498fa5d-77df-4f1c-b076-ea7bc382ccb0)

Here, if we found no error like 

Crash Loop Back Off or Image Pull back error 

our 1st approch should be, describe the deployment and find error.

2nd approach to check logs of deployement

3rd approach check events

  kubectl get events --sort-by=.metadata.creationTimestamp

So get the event and try to troubleshoot the error, In this case we need to increase the namespace memory allocations.


**Crash Loop Back Off**

This error occur on runtime when runtime configration not working.

Another example suppose we have python application is it working fine but it is trying to write on a folder which does not exist, or trying to write on folder which does not have permission to write.

If there is an error with liveness probe it shows the same error.

Example:
vim dep.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx-container
        image: nginx:latest
        command: ["sh", "test.sh"]
        securityContext:
          runAsUser: 1001
        volumeMounts:
        - name: scripts
          mountPath: /app
      volumes:
      - name: scripts
        emptyDir: {}

vim test.sh

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/1e1a3436-9342-4093-a03a-42ce47d28278)

Here in above scenerio user 1001 cannot write at /etc/ path due to insufficient permission, so the container trying again and again and going into Crash state.

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/20ce6dfa-8207-48a9-aec9-e20adf3b1f7e)

# Pods gone into Pending state

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/ebcc9438-1484-49ac-b1b6-ca3f8a9a5859)

  kubectl describe pod ckaexam

  ![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/bccc7440-475d-40a3-8a55-a07b410531b9)

  Two other tains are scheduled, run below command this will un-taint the node

  kubectl taint node kube-node2 cka=test:NoSchedule-

  

**OOM Killed - Out of Memory 

OOM Killed - Limit Overcommit 

OOM Killed - Container Limit Reached**


![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/9b6756e5-26ee-4dd4-bc34-0d0a9dfd442c)



**The connection to the server localhost:8080 was refused - did you specify the right host or port?**

cat /etc/kubernetes/manifest/kube-apiserver.yaml

- --advertise-address=<IP ADDRESS>
- --secure-port=<PORT NO.>

**How to change config, if there is any mismatch**

**Home directory of user have hidden directory called **.kube** change the following here**

cat .kube/config

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/7b4adbc8-e656-4232-b7f8-938fc85346cb)

**Might possible that API server is not running, check with kubelet service**

systemctl status kubelet
systemctl restart kubelet
systemctl enable kubelet --now

**Check Logs, On every worker node log directory created.**

cd /var/log/pods
ls -lrth 

**Restart kube-api server if found any error.** Restart a service means restart pods

method 1 - mv  kube-apiserver.yaml /tmp

again move back to home location 

mv /tmp/kube-apiserver.yaml .

=========================================================================================================================

**Secured sensitive information on Kubernetes cluster**

* Kyverno, RBAC, Secure your API server, Cluster network policies are very well defined, Information (Data) are encrypted at REST in ETCD, Use Secure container Images, Cluster Monitoring, Frequent Upgrades.


# Jenkins CICD Pipeline

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


# D2D Tasks:

1. Observability and Monitoring: Start the day from going through the email if we have an email related to any critical alerts so we start work upon it and if there is any warning alert on the cluster to we check the warnings.
2. Requirement Check: Check if there any requirement for Patching (upgrade any node through yum or any service version upgrade called patching) or if there is new version available which we need to upgrade in EKS of kubernetes so we raise a ticket and start working on it.
3. Billing Review: We generate the monthly billing report and share with the higher management to review of monthly Aws Cloud enviroment.
4. Security Issues: D2D work upon the Aws cloud landing zone where we identify and mitigate if there is any security breach in our cluster example any security group have created for the application which having unnecessary ports open so we give a check on that using services like Security Hub and AWS Trusted Advisor.
5. Monitoring: We have setup Cloudwatch dashboard for our different application we provide that dashboard to application team we also have configured alarms and alerts as well using SES and SNS



Aws Landing Zone ?
* Which Aws instance (flavour) and how many is used to support Cloudera cluster ?
* How many pods we can create in __ type of instance and __ size if we have these much of nodes ?
* How much pods EKS supports per worker node ?
* Cloudwatch, SNS, SES 










 
     
