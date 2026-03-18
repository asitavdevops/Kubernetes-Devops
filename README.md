# Kubernetes-Devops (K8 concepts and All Projects)

**Docker vs Kubernetes – Why Kubernetes is Needed?**
Docker does not support the issues like mention below and which solution provided by K8s
1. **Single host issue**
Docker works on a single host (one server).
If that server goes down → all containers go down.
Note- Kubernetes solves this by using a cluster (group of nodes).
If one node fails → application runs on other nodes (high availability).
**2. No auto-healing**
In Docker, if a container crashes → it will not recover automatically.
Note- Kubernetes provides auto-healing using:
ReplicaSet / Deployment
It automatically restarts or replaces failed containers.
**3.No auto-scaling**
Docker cannot handle traffic increase automatically.
Kubernetes solves this using:
HPA (Horizontal Pod Autoscaler)
It increases or decreases pods based on traffic/load.
**4. Lack of enterprise features**
Docker alone does not provide:
Load balancing
Rolling updates
Service discovery
**Kubernetes provides all these enterprise-level features:**

**Kubernates Archchitecture:**
User → Control Plane → Worker Node → Pod → Container (Ref Kubernates-Architecture)

Lets start creating of a container , on top of VM we run a container with command docker run -dit -v asitav:/app --name=c1 nginx
So if we will simplly run any container nothing will happen let say we are running jave based application in the container
then midatotary we need java run time(JVM) to run the java application same way in docker container behind the scean we have docker run time(Container Runtime (containerd / CRI-O)) which is called dockersim.
that is responsibe to run the container .  In Kubernates we create Master and Worker (In Production we have multiple Master and multiple worker architecture).
In Kubernates we are not directly sending the request to Workers but your request will go throuth Master which is called Control plane , So when we deploy POD(similar to container)
it gets created in Worker node . 
Control Plane (Master) This is the brain and it Decides: Where to run container,When to create/delete pods,Maintains cluster state
Worker Node (Data Plane):This is where actual app runs
In POD we have 3 component which gets created in Worker node.
1. Kubelet - Its is responsible maitaining the K8 pod, like if its running or not if not running then  as it has a feature of auto healing then inform k8 that the pod is not running .
2. container Runtime - In side K8 POD we will be having container so we need container run time to run the container .But only difference is in K8 docker is not mandatory 
	Either we can use dockersim , containerd,crio all are compitaror so insread of using dockersim we can use any other container runtime which impliments kubernates container interface.
3. kube-proxy - handles networking and load balancing,this is basically provides you networking every pod that we are creating it has to be allocated with some ip address and load balancing capablities 

 Pod: Smallest unit in Kubernetes , Contains one or more containers,Pod = Wrapper around container
 Kubelet:Agent inside node,Talks to control plane,Ensures pod is running
 Container Runtime:Actually runs containers
 Easy Analogy (Best for Remembering) : 
 Control Plane = Manager
 Worker Node = Employees
 Pod = Task
 Container = Actual work



