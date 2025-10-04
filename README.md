# Terraform

Q: Difference between for_each and for_in in Terraform?

- For_each: is used when you want to create multiple instance of a resource. Suppose you want to create three S3 buckets so instead of writing the resource block 3 times, you can simply use "for_each" inside that resource block.

<img width="829" height="197" alt="image" src="https://github.com/user-attachments/assets/122c76f0-7826-454e-8154-23f2e951a794" />

- For_in: It is exactly same as loop in python or shell script. It will loop over variables, same in terraform as well.

<img width="959" height="175" alt="image" src="https://github.com/user-attachments/assets/91482b34-a1cc-4cb0-b4ba-99f459e9f9b8" />

Q: How do Terraform modules work and why should we use them?

- Modules are re-usable groups in terraform. They are just like functions in python.
- In a current org I work with multiple development teams and all of them need VPC resource on Aws.
- Instead of writing hundred lines of VPC creation every time, I will just define a module for VPC, when the next requirement comes I just invoke the module in my terraform file by just passing the parameters.
- Suppose with vpc creation we got a requirement of 10 subnet, security groups, ec2 instances and some s3 buckets image the lines we have to write instead of that we can create a module and just change the value of variables.
- We can share the document with the development teams and they even can easily update values they want to change and use the module.
- Advantages: Re-usability, maintenence become easy.

Q: What is state file in Terraform?

- State file is the brain of the terraform.
- Whenever terraform creates a resource on a cloud provider like Aws, terraform store this information on to the state file to understand what resource it has to be created.
- Simple, every time we create a resource in terraform it store the information in state file as.

  1. Resource ID
  2. Metadata
  3. Ip address
  4. Last known state

- When we try to update anything it compare with the last state and the current things we are asking to update.
- If state file is not present or deleted or moved then similar resource will created multiple times.

Q: Have you considered storing statefile in Git instead of Aws S3 or Azure Blob?

- In terraform, state file holds the critical information like resource id, last known state, metadata, Ipaddress, dependencies.
- This cannot stored on the local system of any devops engineer.
- Also, this cannot stored on git repository.
- If git repo is public people can have access to the state file easily, even it is private withing the organization, still some people can have access.
- To avoid this, remote file is stored in remote backend like Aws S3 or Azure Blob or GCS.
- Define a backend.tf within the HCL file in the backend.tf file we will define the remote backend.
- We can have versioning enable for the backend.
- We can increase the security of state file through access level in S3.
- We can block access with strict policies.
- We can enable backups and lockings of the state file as multiple people cannot run the terraform at same time.

Q: How do you manage state file in Terraform?

- Statefile is the brain of the terraform. Statefile has a information of the resources that we created in Terraform.
- We have to keep state file at the centralized location where other engineers can also access it like remote backend (Aws S3).


Q: Two devops engineers executed terraform apply at once.

- In terraform there is a concept called 'state locking' and we store the state file in remote backend S3 and S3 also implement locking of the state file.
- If both the engineers have run 'terraform apply' at same time considering some latency in the network, S3 provide the lock whose request reach 1st to the remote backend.
- If other engineer is requested for the same modification, he/she might see the resource already exist.

Q: We don't have a cloud account where do we store the state file?

- Remote backend concept of terraform is not restricted to the cloud providers.
- Terraform also supports stand alone backend concepts like Hashicorp consul.
- We can install hashicorp consul and integrate with hashicorp vault.
- Otherwise, if you are ok with the Terraform enterprise version with licensing cost then you can get state file locking feature along with other features like drift detection.

Q: Write terraform code to create any terraform resource on Aws.

Q: Difference between resource and data-source in Terraform?

- Terraform can not only create, delete, modify information on the cloud provider but it also can read information from the cloud provider using "data-source"
- For that, first, we have define a data block


<img width="661" height="185" alt="image" src="https://github.com/user-attachments/assets/617c53bd-c0ee-49e3-a52c-e7db209f6e74" />

- Then define what you want terraform to read example subnet_id below, here we are fetching infomation of "default_route_table_id"

<img width="1477" height="258" alt="image" src="https://github.com/user-attachments/assets/8472f192-2bfd-47fb-b5e8-bf23c0cfaf4e" />

- This information we can get through terraform documentaion: Aws Provider -> Data sources


===========================================================================================
# Monitoring with Grafana and Prometheus

* What are challenges with Prometheus?


===========================================================================================
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
  

===========================================================================================
# AWS

1. Explain how will you design a highly available and scalable multi-tier application.

2. What is Nat and when it is used?
- Nat in Aws is used to allow resources in private subnet to initiate internet connection while still being protected from the incomming traffic.

3. Can applications in different subnets of Vpc interact by default, if no, Why?
- When we create a Vpc, aws create a default route also called as main route, this route has a target as a local, means applications of different subnet within the vpc should interact with each other.
- By default it is enabled for internal communication and external communication is disabled for that Nat is used.
- To block any request NACL is used but by default is not blocked by Aws.

4. NACL vs Security group, which one do you use in your organization?
- When we create a VPC in Aws a route rule of VPC will allow communication between subnets of Aws because the default route rule.
- By default when we configure an NACL all the traffic is denied, if we want to allow some port or IP we have to specify. NACL works on the subnet level.
- Security groups works on the Instance level if we want to allow any traffic from port or IP, if we don't allow any traffic by default it is denied.
- NACL is stateless, Security group is statefull
- Stateless: We have define a rule weather allow or deny for both ingress or egress,
- Statefull: We only have to define a rule for ingress, for egress all the traffic is allow by default.

5. Ec2 instance is crashed unexpectedly, How will you troubleshoot?
- In Aws we have service cloud "Cloud Trail". With the help of cloudtrail we can find out what can be the potential issue.
- Specifically Ec2 is terminated we will look for an API call called "Terminate Instances" in Cloud Trail.
- Another thing we can look for, if the Ec2 instance is a spot instance, spot instance is used to save money in many org.
- Another thing we can look for if the instance is terminated through auto scaling group.
- All of these thing can be looked in Cloud Trail.

6. Lambda function faild randomly, with no error logs. How will you fix?
- Lambda function usually performs a HTTP request to interact with other Aws services like S3 or RDS.
- We will definetely find an error in logs but we have to look for it.
- To understand the complete journey of the request we will enable tracing for this function and this can be enabled by Aws X-ray service.
- Then through x-ray service we'll try to understand if there is any call latency with any service like S3 or Rds.
- As an immediate fix, we can increase the number of retries so it will try once or twice to run or just run the request in loop within the lambda function.
- We can increase the timeout of lambda function, if it is genuinely failing with timeout.
- Still if its failing after increase the timeout we will re-create the lamba or may be choose some other programming language.

7. What will you do when Aws RDS storage is full?
- List of steps to take to solve the problem in long term:
- We assume that users are already blocked and unable to login due to storage is full.
- We will go to RDS and try to take snapshot just to be secure.
- We will create a larger storage this time, bit larger than the previous one
- We will try to enable auto-scaling. This will temporary un-block the users.
- As a long term solution: We will go to RDS and look for database being used, tables and objects that is consuming large storage in the Rds storage.
- We will run a sql query, in case we are using any other db we'll use that language to identify which database is consuming large storage.
- We will share this information to the developers or other stake holders and check if we can drop the table or remove the database or ask them to housekeep the specific db or remove the duplicate db or table.
- For future we will head to the cloud watch and create a metric to monitor the Rds storage called as "free storage space". This will inform us when Rds storage is about to full.

8. A developer deleted critical resources like S3, Rds, Ec2. What you will do?
- Two things to need to address here: Instant solution and Long term solution.
- Because the critical resource is deleted. I will try to re-create the resource.
- Fortunately these resources have a backup mechanism like S3 have versioning, Ec2 have snapshots or Ami's, Rds have "Point In time recovery" (PITR). We will try to restore the backup first.
- Afcourse, some data will be loss while re-creating the resource from previous version still I will go ahead and create.
- All the above is a instant solution.
- Long term solution for this is to create a strong IAM policies or RBAC rules.
- I will follow a zero privilege approach or only right people have access to the resources.
- Also we will try to use a IAC approach like modify the infra with the terraform and integrated with version control system like Git for proper audting and versioning.


9. Explain a cost optimization activity that you perform in the current or last org?
- Cost optimization is part of my day-to-day roles.
- I was working on the task where I was identifying the un-used EBS volumes and delete those un-used EBS volumes.
- Before I used to work on aws cli to run "aws describe volumes" to identify the list of volumes but I realized the Lambda function is the better approach where I used python as a scripting language.
- I try to look for un-used volumes by using the boto3 module and delete the same by using boto3 itself.
- I run the function periodically so I don't need to remember that I need to run the lambda function. This will be executed every 4th Friday of the month.

10. Explain recent challenge that you faced that you faced with Aws and how did you solve it?
- In recent time I faced the major challenge with Aws code commit as Aws annonce the 








* Aws Landing Zone ?
* Which Aws instance (flavour) and how many is used to support Cloudera cluster ?
* How many pods we can create in __ type of instance and __ size if we have these much of nodes ?
* How much pods EKS supports per worker node ?
* Cloudwatch, SNS, SES
* difference in aws auto scaling vs ec2 auto scaling
* difference in launch template vs launch configuration
* who is publisher and who is consumer (sqs)
* cloudfront - uses and need - Cloud Front is a caching service or a content delivery network where response of the request are cached at a location to reduce the latency.
* Regional Egde cache in Cloud Front - A regional edge cache in Amazon CloudFront is a location that's deployed globally, close to viewers. They're located between the origin server and the global edge locations (PoPs).
* Geo Targeting in Cloud Front? - Geo-targeting in Amazon CloudFront is a feature that allows businesses to show personalized content to their audience based on their geographic location.
* when to choose s3 and when to cloudfront
* Iam roles vs policy
* aws lambda - use case
* lambda edge
* vertical scaling in lambda
===========================================================================================
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
===========================================================================================

# Docker

Q: You have just build docker image and run it using docker run, but the container exist immediately after starting. What might be the reason? How would you troubleshoot and fix the issue?

- Docker containers are meant to be a single process containers. If the command or process specified in the containers completes quickly or may be it fails immediately or if its not a long running process. Then the container might exit right after the container started.
- For example, we run a command in the container called "echo, Hello World" so echo is a linux command which run and complete in a second and the life of the process is very short.
- Right after executing the command the container exits.
- Check docker log when container fails

Q: What is the purpose of EXPOSE keyword in Dockerfile? 

- Practical use case of "EXPOSE" keyword is just for documentation purpose. Dockerfile allows documentation of the port using expose instruction.
- Example, you are working on a docker file and year later you want to handover this docker file to other devops engineer.
- Expose keyword will help other devops engineer to understand that your application is running on port 80.
- Otherwise they have to check the source code and findout on which port the app is running which is not an easy task.
- In reality, to expose any port we use '-p' parameter.
- EXPOSE comes handy only with docker compose, in docker compose we use expose with port number (EXPOSE 8080) so docker compose will understand that we want to expose the port.


Q: Port is not accessible even after Port mapping in Docker | You're running a Docker container, but when you try to access the application via localhost: <port>, nothing loads to timeout?

- First, In the question itself mentioned that port mapping is done so this is not the possibility of error.
- Re-check, if at the time of 'docker run' right port is used, there might a issue with port forwarding.
- I will check if the port is free or not used with any other service.
- I will check if there is any firewall settings configured, like port is blocked by the firewall.
- I will try to understand on which language the app is written, suppose python, so there might be a chances where developer mentioned "app.listen.(80,127.0.0.1)"
- Above, port is mapped with localhost means if we run "curl localhost:8080" it will work but outside the cluster it will not work.
- Simply, ask the developer to mapped the port with "app.listen.(80,0.0.0.0/0)
- Further check 'docker log', 'docker inspect', 'netstat', 'lsof'


Q: Data lost when container stops and restarts, How will you fix it?

- By default, containers are ephimeral in nature and anything stored inside the container will be lost when container is dead.
- Suppose MYSQL application inside the container is writing files, so data will be lost by default if the container is restarted.
- We can use the concept of "docker volumes" to preserve the data in containers.

		docker volume create <volume name>
		docker volume create mydata
		docker run -v mydata:/app/data nginx	# nginx is the name of the container

- Next time, when container is dead and restarted. It will take the data from mydata volume
 
Q: You made the change in the code, re-build the image but the change isn't reflected?

- Suppose, there's some payment application which is running fine, a developer made a change in version 1.
- After making the change in the code, developer saved the code and ran the command I gave "docker build -t V2 <docker file location>"
- V2 image is created, developer shared the image to QE team, QE team says that application is working same like V1 and no change happend.
- Now this situation comes to us as an devops engineer, now handle the situation.
- Answer: This happens due to caching. Instructions within the dockerfile is layered and cache is maintained by docker.
- In some cases, Docker might not recognize the change at a particular instruction level in the Docker, because of that it will not re-build that particular part, but it will just take the layer.
- This situation happens very rarely but when it happens but when this happens we just need to run below command.

		docker build --no-cache -t <image-name> <location of Docker file>

- This happens because docker uses caching to build the image, suppose we build same image multiple times, 1st time it will take 10 minutes, 2nd time it will take 5 minutes because it cache the layers.

Q: Appication works locally but inside the container it fails and crashes with "Permission Denied". What could be wrong?

- When we run "docker build" this command is ran by some user, we cannot run this by user root, this is a bad practise.
- Within the docker file we use users like 'ubuntu' or 'sunny', these users have elevated privileges (higher-than-normal administrative rights and permissions).

<img width="872" height="733" alt="image" src="https://github.com/user-attachments/assets/91018633-e4c9-4fcf-bacb-e3da1899d22b" />

- As stated in the above snap, the user is created named 'appuser'
- If we don't mention any user in the docker file 'root' user will be considered and may be the appuser does not have permission to execute the application.

Q: Docker host is running out of disk space. How do you clean up?

	docker system df
	docker system prune

- Above, 'prune' command is used to clean up dangling images and df is to check the status.
- Dangling images: Images that are no longer referenced by any tags or active containers. They are essentially orphaned image layers that remain on the system but are not actively in use or easily identifiable by a name and tag.
- 




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





===========================================================================================
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

1. Cluster IP - Kubernetes service can only be accessible within the cluster. Any pod within the K8 cluster in any namespace can access the service using cluster IP or DNS name assocaite with the service. Scope of access is internal.
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
- There is a payment namespace
- Also, there are 3 microservices (pods) in a namespace along with mysql DB which hold a critical information.
- So, requirement is mysql DB should be accessible only from Pod A rest 2 pods should not be talk to mysql DB via any medium.
- This can be possible through "Network Policies"
- Using network policies we can block access to a pod or restrict it only from certain pods.

Steps:

* First, Label the DB pods as "app: db"
* Then, application pod which wants to access the DB label it as "app: myapp"

<img width="674" height="565" alt="image" src="https://github.com/user-attachments/assets/ca1101ee-e0d9-48cd-94bc-85a700020313" />

* Create a network policy, which only allow access to DB which has a particular label as "app: myapp" and "app: db"

<img width="924" height="750" alt="image" src="https://github.com/user-attachments/assets/4bec0a9f-4d6a-4b67-a7d8-0a1f5eb84f0e" />


Q: Explain the Deployment strategy that you follow in your organinzation?

- There are 2 popular deployment strategies:

1. Canary
2. Blue Green

* We follow Canary deployment strategy in current organinzation.
* We roll out 10% traffic to new version of the application.
* Remaining 90% users still uses the old version.
* We take feedback from the 10% of the users and run some test cases for load stimulation.
* After couple of days we increase the laod to 20%, 50% and gradually 100%
* Then we delete the old version of the application.
* Traditionally we have ingress resource, service and Pod.
* For new version of the app we need new ingress resource, service and Pod.
* Adding annotations to the new ingress stating 10% of the traffic should go to this ingress.
* Ingress controller configures the load balancer and tells the load balancer forward 90% of traffic to the old ingress and 10% to new.
* Once all traffic is routed to new ingress we will delete the old ingress.


Q: Rollback strategy that you follow in your organization?

- We follow Canary model of deployment where we gradually rollout new version of the application to the customers.
- Initially the new version of the applicaion is only rolled out to 10% of users and rest are using old version of the application, then we gradually changed to 20%, 50% and 100%.
- Suppose due to some reason still we faced issue in the production we will follow a "Rollback strategy"
- Because we follow GitOps approach all our manifest are available in git repository.
- So I revert Helm chart to the previous version, it made a change to git repository.
- Because, ArgoCD is watching git repo and auto sync is enabled on Argo it will pick automatically the old version of helm chart and deploy on kubernetes cluster.
- But, we try to avoid situations of rollbacks by following proper deployment strategies.

 Q: Design a solution to avoid rollbacks?

 - Here, interviewer is asking a deployment strategy.
 - In our current organization we have already design such solution, so we follow canary model of deployment.
 - As canary model we rollout new version of the application only to 10% of people for the first time.
 - Gradually we increase the load %
 - Becuase we follow this deployment strategy any issue can be caught at the early stages itself.
 - Before going 100% live we take feedback on different layers.
 - This is how we eliminate scenerios or rollbacks.


Q: Explain the role of coreDNS in Kubernetes?

- Core DNS takes care DNS in Kubernetes. It is the default DNS server on the K8 cluster.
- It takes care of domain to ip address translation.
- Example: Pod A needs to communicate with payment micro-service, so in pod's env variable or config map we use a dns name like "payment.default.svc.cluster.local"
- When pod tries to communicate with DNS name, this DNS name is resolved to an IP address like 10.96.1.5
- This resolution in K8 is performed by Core DNS.  

Q: If a node is tainted as 'NoSchedule'. Can you still schedule a pod on a node?

- Taint is basically marking a node that no pod is schedule on that node, so in this case it is marked as "No schedule"
- Reason, may the node is control plane or may be some maintainence activity is scheduled for that node.
- This is possible when we go with tolerations.
- Taints are applied to nodes to hold-off specific pods unless those pods have a matching toleration.
- Tolerations are applied to pods, allowing them to bypass taints and run on tainted nodes.
- Kubernetes supports three taint effects:

1. NoSchedule → Pod will not scheduled on the node unless they have a matching toleration.
2. PreferNoSchedule → System will try to avoid placing a pod on a node, but does not gaurantee it.
3. NoExecute → Immediately evicts existing pods unless they have a matching toleration.

- Imparitive command - taints (Node level):

	kubectl describe node node01 | grep Taints*			# check if any taints exists on a node.
	kubectl taint nodes node-name key=value:taint-effect
	kubectl taint nodes node01 app=blue:NoSchedule
	kubectl taint node node01 spray=mortein:NoSchedule

- Tolerations:

     	apiVersion: v1
     	kind: Pod
     	metadata:
     	  name: bee
     	spec:
     	  containers:
     	  - image: nginx
     	    name: bee
     	  tolerations:
     	  - key: "spray"
     	    value: "mortein"
              operator: "Equal"
     	    effect: NoSchedule
     	    

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
- Kyverno is a policy engine for Kubernetes that helps platform engineering teams manage security, compliance, and governance.
- It runs as a dynamic admission controller in a Kubernetes cluster, receiving HTTP callbacks from the Kubernetes API server and applying policies to enforce admission policies or reject requests. 


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


Q: ImagePullBackOff / ErrImagePull / Invalid Image Name Error?

- Some scenerios can be there:
1. Image is not present in a repository like Docker Hub.
2. Image name is written wrong.
3. Image is Private and you don't have access to the registry (Permission Denied).

- Practical:-

     kubectl create deployment nginx-deploy --image=nginx 
     kubectl get pod -w
     kubectl describe pod nginx-deploy..

* Till above everything was fine, we have make error as image does not exit

     kubectl edit deployment nginx-deploy

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/dc16f29b-2f71-4266-95d7-c15b24d33f26)

     kubectl get pods -w 

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/6f45b815-6a33-4507-a671-1c87be22b302)

Q: Crash Loop Back Off error ?

- This is not an error actually this is a state in Kubernetes.
- This occurs when for some reason or for some error your pod is continuesly crashing.
- This occurs on runtime when runtime configration not working.
- Suppose we have python application it is working fine but it is trying to write on a folder which does not exist, or trying to write on folder which does not have permission to write.
- There might be a issue with the Liveness probe as well. Liveness probe checks if the application is Live.
- Troubleshooting steps:

  1. Check "kubectl log pod nginx"
  2. Check "kubectl describe pod" if it shows any signs of error in the events.

- Below snap, it might be issue with the path: /health

<img width="1042" height="652" alt="image" src="https://github.com/user-attachments/assets/71a3f029-82fa-4adb-8ccf-697d5c70dff2" />

- Depending upon the error we will work upon the solution.

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

- Here in above scenerio user 1001 cannot write at /etc/ path due to insufficient permission, so the container trying again and again and going into Crash state.

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/20ce6dfa-8207-48a9-aec9-e20adf3b1f7e)

Q: Difference between liveness and readiness probe?

- Liveness is used to check if container or application running in the pod is alive or not.
- Take example of a load balancer. LB is tied to a target group. TG has couple of virtual machines.
- LB balance the request between virtual machines but LB also keeps checking if the vm's are healthy or not. It only sends requests to vm which is healthy.
- We need a mechanism to restart a crashed container. In kubernetes we have same kind of mechanism called liveness probe. 
- Readiness probe checks if the application or pod is ready to receive the traffic or not.
- Explanation:

  * Liveness and Readiness are 2 probes can be configured within the pod definition Liveness is configured to see if the pod is alive or not and Readiness is configured to see that same is ready to serve the traffic or not. Because there might be chances that pod is showing ready but not accepting traffic due to it failed.
 

Q: Explain the difference between Ingress and LB service type?

- Both, Ingress and load balancer service type is used to expose the application to the external world and to allow public access to the application.
- When we go for LB service type, for every service that you need to expose, a unique load balancer is created that will increase the cost of the organization. Suppose you are 10 services means 10 load balancer will be created in Aws also we don't have a control on the load balancer it is up to CCM of kubernetes to decide which load balancer is created.
- Ingress also exposes the application to the external world but it provides lot of configuration options, for multiple service we can use the same load balancer.
- We can create target group in the load balancer using the ingress resource so that request is routed from the load balancer to multiple service backends.
- This way ingress is quite effictive for the organization.
- Along with that we can customize the ingress resource, we can choose the type of load balancer using ingress controller also we can choose the load balancer technique as well, like host based, path based, weight based laod balancing.
- There are multiple ingress controller in the market like nginx, traffic, nvoy.

Q: Your application working fine with ClusterIP with Ingress. How do you troubleshoot?

- Here we have 2 things to understand.

  1. Cluster IP working means communincation is done by cluster level only, may a different pod is trying to access the pod via service.
  2. Ingress is not working means communication is tried from external world through some DNS endpoint.

- Troubleshoot:

1. Check if the Ingress controller is installed or not: Ingress controller is the one who watch the ingress resource and created the LB. Users actually makes the request to load balancer and from LB request is served to the NodePort.
2. Check Ingress controller logs: We must find traces of the Ingress controller in the logs.
3. Ingress class Name: When there are multiple ingress controller in the kubernetes cluster we need to define which ingress controller will watch which ingress controller. Ingress resources are setup with feild called "Ingress class name"
4. If all the above is correct check for the YAML file for the ingress. May be you configured wrong service or port as backend in ingress.


Q: Why do I need to setup Ingress controller after creating ingress?

- Likewise, a deployment is created so a replica set controller is watching the deployment and create or delete the replicas.
- Similarly we create Ingress with "kind: Ingress".
- But, we have to installed our choice of Ingress controller who can watch this Ingress resource and configure load balancer for us.

Q: We have an inhouse load balancer, Can we use ingress with our load balancers?

- Likewise, If we create a Ingress resource it does not work if we don't install Ingress controller.
- Similarly a company can use their in-house load balancer but they have to install the Ingress controller for the same.
- Using Operators one can easily create their own kubernetes controllers and use their own load balancers.

Q: Your deployment has 3 replicas but only 1 pod is running. What could be wrong?

- Out of 3 replicas 1 replica is running so we will eliminate the common issue possibility like "image not found", "Imagepullsecret", "Crashloopbackoff".
- Possible reason for the issue is "Lack of resources"
- Suppose the failed pods are looking for 4 cpu but the available nodes have only 2-2 cpu's
- Other possible reason is Nodes are tainted. So we have to apply tolerations to the nodes to schedule a pods
- Check for pod configuration if there is any request for more cpu or taints have applied, then go for describe pod or check pod events for historical events.
- Solution for this we have to add new node on the cluster.

Q: Your pod mounts a ConfigMap, but changes to the configmap are not reflected?

Q: Explain Node Affinity?

- Node affinity is a way to influence the pods scheduling.
- It tells kubernetes which nodes a pod prefers or requires to run on, based on labels assigned on the nodes.
- Suppose, 3 nodes in the cluster, 2 is cpu based and 1 is GPU based.
- Based on our workload we want our pods to schedule only on GPU node.
- Node affinity comes in two main types:

  1. required during scheduling: This is a preference rather than a strict requirement (Hard Affinity). The scheduler will try to place the pod on nodes that satisfy the conditions, but if no such nodes are available, the pod can still be scheduled on other nodes. You can assign a weight to preferred rules, allowing you to prioritize certain preferences over others. Similar to hard affinity, ignoredDuringExecution means label changes after scheduling do not impact running pods.The pod will only be scheduled on nodes that satisfy all the specified label matching conditions. If no matching node is found, the pod will remain in a Pending state until a suitable node becomes available. IgnoredDuringExecution means that if a node's labels change after the pod has been scheduled, the running pod is not affected. It will not be evicted or rescheduled.

  2. preferredDuringScheduling: This is a preference rather than a strict requirement. The scheduler will try to place the pod on nodes that satisfy the conditions, but if no such nodes are available, the pod can still be scheduled on other nodes. You can assign a weight to preferred rules, allowing you to prioritize certain preferences over others. Similar to hard affinity, ignoredDuringExecution means label changes after scheduling do not impact running pods.


Q: Difference between NodeAffinity and Node label selector?

- Node Affinity is a modern version of Nodelabelselector. Node affinity comes with Hard and Soft Affinity.
- Hard Affinity: I can tell kubernetes to only schedule my pod at this particular pod only.
- Soft Affinity: I can tell kubernetes I am preffering to schedule my pod at this particular pod only. Otherwise I am fine if pod is schedule on some other node.

Q: What is container runtime in Kubernetes?

- It is a component of Kubernetes worker node and it is present on all the worker nodes.
- When API server calls at the time we run "kubectl" command. API checks for authenticaiton & authorization.
- Scheduler identifies right node to place the pod. Once done, scheduler talks to kubelet to place the pod.
- Then, kubelet calls the "Container Runtime". It not only runs the container but follows the series of steps:

1. CR pulls the image that is provided in the pod specification, it looks for the container registry like Dockerhub.
2. Once the image is pulled it create the linux namespace for the container. It defines the Cgroups & all the kernel premitive to run the container.
3. Finally, it runs the container within the pod.


Q: Pods gone into Pending state

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/ebcc9438-1484-49ac-b1b6-ca3f8a9a5859)

  kubectl describe pod ckaexam

  ![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/bccc7440-475d-40a3-8a55-a07b410531b9)

* Two other tains are scheduled, run below command this will un-taint the node

		kubectl taint node kube-node2 cka=test:NoSchedule-

  
Q: OOM Killed - Out of Memory | Limit Overcommit | Container Limit Reached

![image](https://github.com/sunnyvalechha/Devops-inter-prep/assets/59471885/9b6756e5-26ee-4dd4-bc34-0d0a9dfd442c)

Q: The connection to the server localhost:8080 was refused - did you specify the right host or port?

		cat /etc/kubernetes/manifest/kube-apiserver.yaml
		--advertise-address=<IP ADDRESS>
  		--secure-port=<PORT NO.>

Q: How to change config, if there is any mismatch?

* Home directory of user have hidden directory called **.kube** change the following here

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



Q: Secured sensitive information on Kubernetes cluster?

* Kyverno, RBAC, Secure your API server, Cluster network policies are very well defined, Information (Data) are encrypted at REST in ETCD, Use Secure container Images, Cluster Monitoring, Frequent Upgrades.


===========================================================================================
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

# Software Development Life cycle (SDLC)

* There are 3 major phases of SDLC -  Design, Development, and Test

Example: 
1. There is an E-commerce website called Flipkart or Amazon and the website has the requirement to add a kids section on their website.
2. So 1st phase is gather requirement.
3. 2nd phase will be planning.
4. 3rd phase is defining.
5. 4th phase is designing
6. Building
7. Testing
8. Deploy

![image](https://github.com/user-attachments/assets/b3cc149e-5963-4d4e-91c0-df7b8b727433)

These days every organization follows the Agile methodology.

* Agile methodology: In Agile we follow all the above steps but we do not wait till all the planning is done, hence we will take short sprints like don't wait till all the design documents are done, if the small chunk is done we start the process then again there is the progress we again build.


**Promote application from Dev env to Production env**

===========================================================================================
# D2D Tasks:

1. Observability and Monitoring: Start the day from going through the email if we have an email related to any critical alerts so we start work upon it and if there is any warning alert on the cluster to we check the warnings.
2. Requirement Check: Check if there any requirement for Patching (upgrade any node through yum or any service version upgrade called patching) or if there is new version available which we need to upgrade in EKS of kubernetes so we raise a ticket and start working on it.
3. Billing Review: We generate the monthly billing report and share with the higher management to review of monthly Aws Cloud enviroment.
4. Security Issues: D2D work upon the Aws cloud landing zone where we identify and mitigate if there is any security breach in our cluster example any security group have created for the application which having unnecessary ports open so we give a check on that using services like Security Hub and AWS Trusted Advisor.
5. Monitoring: We have setup Cloudwatch dashboard for our different application we provide that dashboard to application team we also have configured alarms and alerts as well using SES and SNS










 
     
