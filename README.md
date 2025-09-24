1. What is DevOps?
Ans: It is a culture that improves application delivery by ensuring proper automation, quality checks, monitoring or observability, and testing.
3. Why is DevOps important?
4. Introduce yourself.
Ans: I am working as a DevOps engineer. I have an overall experience of 6 years. I started my career as a System Administrator and Platform engineer, specifically in DevOps, where I have more than 3 years of experience.
6. What are your day-to-day activities?
Ans: In the current organization I take care of the automation part using Ansible.
     I ensure that quality should be maintained for the application.
     I ensure there should be continuous monitoring.
     I have automated the Testing process in the DevOps lifecycle.

# Terraform

1. Migration resource to Terraform. How?
   
# Software Development Lifecycle

There are 3 major phases of SDLC Design, Development, and Test

Example: 
1. There is an E-commerce website called Flipkart or Amazon and the website has the requirement to add a kids section on their website.
2. 1st is requirement.
3. 2nd phase will be planning.
4. 3rd phase is defining.
5. 4th phase is designing
6. Building
7. Testing
8. Deploy

![image](https://github.com/user-attachments/assets/b3cc149e-5963-4d4e-91c0-df7b8b727433)

These days every organization follows the Agile methodology.

* Agile methodology: In Agile we follow all the above steps but we do not wait till all the planning is done, hence we will take short sprints like don't wait till all the design documents are done, if the small chunk is done we start the process then again there is the progress we again build.





   










# Monitoring with Grafana / Prometheus / Thanos

What are challenges with Prometheus? 
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

Q: What is side car container and when to use one?

Q: Dockerfile components?

          FROM ubuntu / Centos / tomcat / golang            # Represent the base Image. This command executes first when we start building the Image.
          VOLUME ["/newdirectory"]                          # Attach a volume inside the container, and with this volume we can attach a local directory called volume mount.
          WORKDIR /app                                           # Once the source code build, will store in this directory
          COPY <source> <destination>                            # Copy the dependencies from local system to image
          RUN apt-get update && pip install requirement.txt      # Execute commands while creating image
          ENTRYPOINT ["python3"]                                 # When we start the container the script or command mentioned here is executed (Cannot over write)
          CMD ["manage.py", "runserver", "0.0.0.0:8000"]         # Start the process inside the container (Can be over write, means if port 8000 is occupied already we can change but if would have mentiond in ENTRYPOINT we cannot change)


Q: Multi-stage builds?
- Practical:

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

* Now use the multi-stage docker build image using Distroless images called SCRATCH
* Build the docker image present at /home/ubuntu/Docker-Zero-to-Hero/examples/golang-multi-stage-docker-build

    sudo docker build -t simple-cal-multi .

![image](https://github.com/user-attachments/assets/26319b06-90ab-43a9-9976-d9a53ace38bf)

* Find: Distroless images on google: Distroless Container Images 






# Kubernetes

- What is the Port range of Service Node-Port?           # 30,000 to 32,767

- Explain kubernetes architecture and its key components?

* Kubernetes architecture is broadly devided into 2 parts:
  1. Control plane / Master component
  2. Data plane / Worker nodes

* Primary component of Control Plane - API server, ETCD, Scheduler, Controler Manager.
* Primary component of Data Plane - Kubelet, Container runtime, Kube proxy.

* When we run a 'kubectl' command to create resources on the kubernetes cluster initially this request sent to API server.     
* API server performs the authentication and authorization.
* If the request is valid, it sends the request to the scheduler.
* Then, scheduler decide on which node the pod has to be scheduled.
* It takes pod affinity, node affinity, taints & tolerations everything into consideration and identifies right nodes for the pod.
* Once the scheduler identifies right node for the pod, API server forward the request to the kubelet on that particular node.
* Kubelet calls container runtime such as docker shim, CRI-o, or container D
* Then, container runtime takes the responsibility to run the container in the pod.
* This is how pod is executed using Kubernetes components.
* Once this kubernetes resource is executed API server passes the information to ETCD.
* And whenever we create a deployment it is maintained by replica set controller, such controller are managed by controller manager component of Kubernetes. 

Q: How various components of Kubernetes interact with each other?
- Here we need to explain what happens when "kubectl apply" command is executed on deployment or on any resource. How any resources is created on cluster?

* "kubectl apply -f deployment.yml" a request is sent to API server component.
* API server perform authenticate & authorization to see if user has right permission to apply configuration.
* If user is authorized to create a pod API server forwards the request to the scheduler.
* Scheduler identifies which node of the k8 cluster is right to place the pod.
* Once the decision is made API server talks to the kubelet on that particular node and runs the pod on that node.
* Then, kubelet invokes container runtime and container runtime takes care to run the container.
* This is how a pod is run on the K8 cluster.
* Once the pod runs, it updates to information on to ETCD that makes the object persistent on the cluster.
* If there is an issue with the pod and pod down the replication controller will create a replica of the pod and this task is done by the controller manager.


Q: What is the purpose of Services in Kubernetes?
A: In K8 service takes cares for a service discovery. 

* E.g., When pod A wants to communicate with pod B, it can't happen with the IP address because pods are ephimeral in nature and if any pod is goes down IP is also changed.
* So both Pod A and B will communicate with service not using the IP address but using Labels and Selectors.
* Because service identifies the pods using labels & selectors. 
* Service acts as a middleman between pods, request from pod A to B is never terminated.
* Services can also help with the default Load balancing through round robin algorithm.
* When there is multiple replicas of a pod, requests has sent to the service and service splits request between multiple replicas of pod.


Q: Why is hardcoding pod IP communication is a bad practise? 
A: A developer is new to K8 and he/she has hardcoded the Ip:

* Frontend is Pod A
* Backend is Pod B
* Developer has hardcoded the IP of Pod B in enviroment variables of Pod A.
* K8 pods are ephimeral in nature. Pods can go down due to lack of resources or crashloopbackoff or any other issue.
* Whenever a pod goes down an Ip of the pod changed. If we hardcode the value of Pod B in pod A's env variable this communication fails and leads to 502 bad gateway error to the clients.
* To avoid this K8 uses a concept called service discovery. Services does not rely on Ip address but it uses a algorithm called Labels & selectors.

Q: Types of Services in Kubernetes?
- Various types of Services in K8 majorily 3 types but it also depends on the scope of access. 

1. Cluster IP - Kubernetes service can only be access within the cluster. Any pod within the K8 cluster in any namespace can access the service using cluster IP or DNS name assocaite with the service. Scope of access is internal.
2. Node Port - Kubernetes exposes special type of port on the K8 node. Access the service with node IP : port number exposed for the service. Scope of access is anyone who has access to the cluster node can access to the service.
3. Load balancer - Enables public access to the K8 services. However LB service type only works on K8 cluster that has Cloud controller manager (CCM) component running on it.
4. ExternalName: This not create a service like above but it enables external access through DNS name.
5. Headless service: When we make cluster IP to none a Headless service is created, commonly used for stateful sets or DNS based service discovery.

Q: What are labels and Selectors in Kubernetes?

- Labels are key value pairs that are used for identification and to grouping of resources.
- Selectors are used for query purpose, services and replicasets use selectors to identify pods using labels.
- Below snapshot we can identify labels with key:value pairs and on the left yaml same selector used to identify the correct pod then service route the traffic as per the labels.

<img width="1800" height="657" alt="image" src="https://github.com/user-attachments/assets/830157c8-d29b-49d6-89b3-e6e16369f856" />


Q: What would you recommend NodePort service or Load balancer type service and why?

- Node Port service and Load balancer service are 2 types of service in Kubernetes.
- There is a fine difference when it comes to Node Port service.
- Node Port service is only accessible using the node IP, followed by the port associated. This means the scope of access is only to the people who can access this K8 node.
- If the nodes are created within virtual private cloud that means people who have access to that VPC can only access service of type NodePort.
- Load balance enables external access to the service.
- Load balancer service type is only available on the kubernetes cluster which have Cloud Controller Manager (CCM) running on it.
- On other clusters without CCM, even if we create service of type LB it will still work as NodePort service so it cannot be accessed outside the K8 cluster.


Q: How Kubernetes Service is related to KubeProxy | How Kube Proxy works with Services?

- In kubernetes primary purpose of services is Service Discovery.
- And, kubernetes uses the concept of Services to communicate with multiple pods.
- Pod A communicate with Service of Pod B and service does not identify the pod using the IP addresses. It uses Labels and Selectors.
- Whenever we create a service, an endpoint is created associated with the IP address, which has the information of the Pods.
- This endpoint is observed by the Kube Proxy.
- Kube Proxy updates IP tables with the information that if request comes to IP "10.96.10.5" which is IP of the service, so forward the request to 2 replicas of Pod.
- Kubernetes service is a resource that can select the pod and it can only work if you have kubeproxy and IP tables.

$ Summary:

- A kubernetes service is created.
- Labels are associated to the pods.
- Selectors are applied to the service.
- Using selectors, service identifies the right pods and kubernetes created endpoint. This endpoint read by Kube Proxy.
- Kube Proxy updates Ip tables.
- Because, the information is updated in the IP tables when request is sent to the service, IP address requests are routed to the replicas of the pods.
- This is how, service and kube proxy work together. 


Q: Disadvantages of service type Load balancer?

- Load balancer service type provisions a seperate external IP's and Load balancer instances for each services.
- Suppose we have 10 services to expose to outside world so it creates 10 load balancers. It will increase the cost the the cloud.
- It will be expensive and inefficient.

Q: What is Headless service in Kubernetes and when did you use it?

- Headless service is a type of service which we created as "Cluster IP" as "None" unlike traditional service it does not Load Balance the request between the pods but it enables Dns A record for each of the pod replica so that one pod can talk to the other pod using the DNS A record name.
- It allows you to directly access the individual pods in a service.
- A headless service does not have a cluster IP assigned to it. Instead of providing a single virtual IP address for the service, a headless service creates a DNS record for each pod associated with the service. These DNS records can then be used to directly address each pod.
- Here, a backend pod want to communicate with the database through service but it should not route the traffic to diffrent pod everytime.
- 1 pod must associate with 1 DB.
- So it will create a DNS A record name that will 

<img width="881" height="458" alt="image" src="https://github.com/user-attachments/assets/8765def1-2cdc-4b1e-8be5-3429cff9e323" />

<img width="540" height="499" alt="image" src="https://github.com/user-attachments/assets/243ed528-ca9e-43fa-a273-92bf153e9d93" />

* Cluster Ip: None
* DNS Name: <pod-name>.<headless-service-name>.<namespace>.svc.cluster.local | myapp-headless.default.svc.cluster.local

Q: Can a Pod access service in different namespace. If yes, How?

- If we create a default service in Kubernetes which is also a least privilege service we can easily access the pod in the cluster be it on any namespace.
- We can access the service by using the name of the service "<pod-name>.<namespace>.svc.cluster.local" | "my-svc.default.svc.cluster.local"

Q: Explain, how you can restrict access to db pod to only one app in the namespace?

Scenerio:
- There are 3 pods in a namespace and 1 
-  


Q: How to Secure Kubernetes Cluster?

1. Secure your API server
2. Secured sensitive information on Kubernetes cluster
3. Very good with RBAC
4. Cluster network policies are very well defined
5. Information (Data) are encrypted at REST in ETCD
6. Use Secure container Images
7. Cluster Monitoring
8. Frequent Upgrades

* Secure your API server: When we run any command let's say 'kubectl get pods' the request first go to API server.
* API server validate with scheduler, but API server is first point of contact.
* So suppose the cluster API server is not secure then the cluster itself can be compromised.
* So as a DevSecOps engineer we have to secure the API server first.
* How we will do that? >> /etc/kubernetes/manifest/kube-apiserserver.yaml
* In kubernetes every resource is a pod and API server should also have a pod / pod file.
* So this kube-api server has a yaml file we have to put TLS certs in the yaml file.
* Then secure this yaml file consist TLS certificates using RBAC

Q: Blue and Green Deployments?


Q: Encrypting Secrets in etcd (Kubernetes Security)?
    
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

Q: Enforce automated k8s cluster security using kyverno generator and ArgoCD?
- Kyverno is a policy engine for Kubernetes that helps platform engineering teams manage security, compliance, and governance. It runs as a dynamic admission controller in a Kubernetes cluster, receiving HTTP callbacks from the Kubernetes API server and applying policies to enforce admission policies or reject requests. 


Q: kubectl apply vs kubectl create?

* When running "kubectl create" command it calls the API server.
* API server then check if the same name available or not (webserver)
* if not it makes the entry in ETCD then ETCD instruct to the scheduler then response goes back to API and then kubelet create a pod on worker node.
* If we have to add a parameter of labels in same configuration again we run 'create' command again and same process repeats but this time we encouter an error called "Pod already exist"
* On the other side "kubectl apply" makes the changes also save the last-applied-configuration time-stamp under annotations and this does not interact with API to make changes instead directly inract with ETCD to update resources this compare Local configuration (yaml file) with Live configuration (kubectl get pod <pod-name> -o yaml). If there is any new changes found it will apply.

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/a806184d-d29a-44a8-b7cb-31ecfa0e323c)

* apply --> used in production
* create --> do not used in prod environment
  
Q: Manually Schedule a Pod?
- To check scheduler running or not, scheduler ran on kube-system namespace

  kubectl get pods -n kube-system

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/f49631fa-c3f0-43c5-a8cb-e9cbc8d80d5c)

* Scheduler running as pod so first we have to stop the scheduler so that it can schedule pod automatically

  mv /etc/kubernetes/manifests/kube-scheduler.yaml /etc/kubernetes/

* So if we run any pod it will go into Pending state because scheduler not present

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/a12cdb30-00a7-437d-8efe-812bd075543e)

* Now we will create a manifest and edit our node manually

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

Q: What is kubernetes and why it is so popular in container orchestration?**
- because in kubernetes we can managed the life cycle for your deployment in a single environment, there are lot of tools like helm charts and custom operators we can write so we can customize our environment, it can be run in any cloud or without cloud we can run the same image in multiple environments.

Q: What is the difference between a Pod and a Deployment in Kubernetes?
- A pod is smallest deployment unit in kubernetes, a pod can contain one or more than container.
- A deployment on the other hand, manages the deployment and scaling of pod. It ensures that specified number of replicas of a pod must running at any time. It also support the rolling update and rollbacks.

Q: How does Kubernetes handle storage, and what are Persistent Volumes (PV) and Persistent Volume Claims (PVC)?
- Persistent volume is a way to define the storage data to the pod. PV is a object in a kubernetes cluster.
- To use Persistent volume it must be requested through Persistent volume clain (PVC). A PVC volume is a request for storage.
- A PVC is used to mount a PV into a pod.
- We can map different classes to different services levels and different backend policies.


Q: Features of Persistent Volume?
- Capacity: Generally a PV will specify storage capacity. This is set by set the storage capacity of PV.
- Volume Models: Kubernetes supports 2 volume modes of Persistent volume. A valid value for volume mode can be either file system or block. Filesystem is the default mode.
- Access Modes:
  1. Read Only Many (ROX) - allows being mounted by multiple nodes in read-only mode.
  2. Read Write Once (RWO) - allows being mounted by a single node in read-write mode.
  3. Read Write Many (RWX) - allow multiple nodes to be mounted in read-write mode.
 

Q: ImagePullBackOff / ErrImagePull / Invalid Image Name Error?
- Two scenerios can be there:
1. Image is not present in a repository like Docker Hub Image name is written wrong mistakenly
2. Image is Private and you don't have access to the registry (Permission Denied).

- Practical:-

     kubectl create deployment nginx-deploy --image=nginx 
     kubectl get pod -w
     kubectl describe pod nginx-deploy..

* Till above everything was fine, we have make error as image does not exit

     kubectl edit deployment nginx-deploy

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/dc16f29b-2f71-4266-95d7-c15b24d33f26)

     kubectl get pods -w 

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/6f45b815-6a33-4507-a671-1c87be22b302)


Q: Resource Quota Namespace?

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

* In above, deployment is created but no pod in ready state, hence nothing found in get pods command 

     kubectl describe deploy nginx-dep -n payments

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/c498fa5d-77df-4f1c-b076-ea7bc382ccb0)

* Here, if we found no error like Crash Loop Back Off or Image Pull back error our 1st approch should be, describe the deployment and find error and 2nd approach to check logs of deployement 3rd approach check events

     kubectl get events --sort-by=.metadata.creationTimestamp

* So get the event and try to troubleshoot the error, In this case we need to increase the namespace memory allocations.


Q: Crash Loop Back Off error ?
- This error occur on runtime when runtime configration not working.
- Another example, suppose we have python application it is working fine but it is trying to write on a folder which does not exist, or trying to write on folder which does not have permission to write.
- If there is an error with liveness probe it shows the same error.

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


# Jenkins & CICD Pipeline

- What type of Jenkins file are you following & Which agent you are using in Jenkins file?
* Declaritive jenkins files and Docker agent as it is light weight in nature also prevents lot of installations. 

- What is difference between Continues Integration and Continues development?

- What is Jenkins declaritive pipeline?

- What are stages and flow of Jenkins CICD pipeline?
* Dev
* Stage
* Prod

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










 
     
