# ia_week4_k8s

# What is Kuberbenetes?

If we consult the official documentation, we will have as a definition:

Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.
(avaiable in: https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/ acess day 07/30/2021 at 09:38 o'clock)

Kubernetes Services eliminate the requisite for manual processes pertaining to cluster-based container systems.

Thus, the K8s(or kubernetes) brings us several advantages of use among them:

![image](https://user-images.githubusercontent.com/83301821/127655700-eee63ab3-d31d-42a2-8be7-212726b3069b.png)

(avaiable in: https://www.veritis.com/wp-content/uploads/2021/01/kubernetes-features.png)

 - Service discovery and load balancing: In addition to the possibility of using a dns to identify the pods, the k8s can also perform load balancing in the application or service.

- Storage orchestration: We can also store persistent application information through volume mounts on the host's filesystem.

- Automated rollouts and rollbacks: Possibility of making a version controlled deployment and ensuring a smoother transition between pods and in case of failure, rollback to the previous state.

- Automatic bin packing: We can limit the amount of resources to be used in each of the applications in order to preserve the integrity of the host machine.

- Self-healing: In case of failure, the container will be replaced by another without compromising the operation.

- Secret and configuration management: Storage of sensitive information without data exposure.

# Kubernetes high-level architecture:

![image](https://user-images.githubusercontent.com/83301821/127657238-705424a9-94e3-4230-be0a-c5a831d73d09.png)

(avaiable in : https://www.veritis.com/wp-content/uploads/2015/06/kubernetes-architecture.png)

- apiserver: It is the frontend of the cluster's. It is through this resource that the state of the cluster is shared and through which all components interact. It also validates and configures object data.

- scheduler: Control plane component that watches for newly created Pods with no assigned node, and selects a node for them to run on.

- etcd: Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data.

- controller-manager: Responsible for controlling nodes, objects, authentications and job's. All control of features and functionality is done in this step.

On worker nodes, we have the following modules running:

- kubelet: It is an agent that runs on each worker node. It is also responsible for passing information from the pod's to the master for proper cluster management.

- kube-proxy: It is the kubernetes proxy service, in addition to being part of the service implementation (we'll talk later), it is responsible for the network communication of the cluster nodes.

- Container-runtime: It is the software that will be responsible for running the containers (in our case the docker).

# What is a Kubeconfig and how to use it [PRACTICE]
Use kubeconfig files to organize information about clusters, users, namespaces, and authentication mechanisms. The ```kubectl``` command-line tool uses kubeconfig files to find the information it needs to choose a cluster and communicate with the API server of a cluster.

![image](https://user-images.githubusercontent.com/83301821/128562451-50dd7b15-a14d-49a2-b6e6-fac3daee53b4.png)

# Working with Kubernetes Objects [PRATICE]:

- Namespace
Kubernetes supports multiple virtual clusters backed by the same physical cluster. These virtual clusters are called namespaces:

![image](https://user-images.githubusercontent.com/83301821/127692276-6f7dd156-9e5a-4e20-ae6e-cc199ff7ce23.png)

If no namespace is created or specified, the default namespace will be used. Kubernetes has a namespace called kube-system that contains the services that run by its architecture (theme already covered in previous topics) that can be viewed with the command above (in which we list all the pods of the namespace in question). Using a namespace, we can manage several desktops on a single machine.

- Pod

It is the smallest deployable object in kubernetes. The pod encapsulates the running container so that k8s manages only the pod and not the container directly. We can define (not in most use cases) more than one container per pod, but by default each pod is analogous to the container.

![image](https://user-images.githubusercontent.com/83301821/127693415-f0cab89b-8d91-4e23-836d-696d6c336164.png)

Above example: list all pods in execution in default namespace

- Deployment

A Deployment provides declarative updates for Pods and ReplicaSets. You describe a desired state in a Deployment, and the Deployment Controller changes the actual state to the desired state at a controlled rate. You can define Deployments to create new ReplicaSets, or to remove existing Deployments and adopt all their resources with new Deployments.

Usage:

![image](https://user-images.githubusercontent.com/83301821/127694399-a6faf081-2a72-4aff-96df-741a11922eec.png)

We write declative scripts that provide update in state of a pod or replicaset. Above, we have the deployment of a frontend application using nginx image and 2 replicas with replicaset.

In this case, we can apply (or create) the script with:
 $ kubectl create -f deployment01.yaml

And we can list the deployment above: 

![image](https://user-images.githubusercontent.com/83301821/127694299-0d05cc51-26cb-43f4-ae7b-1e5193d668a5.png)

- StatefulSet

It is an object used to perform deployment in statefull type applications. In this object, each pod is uniquely mapped. Because here the order of each one of them matters in the application. Thus, this solution is used with PV (persistent volume) to ensure data consistency. One of the features of statefullSet:
 (a) Stable, unique network identifiers.
 (b) Stable, persistent storage.
 (c) Ordered, graceful deployment and scaling.
 (d) Ordered, automated rolling updates.

![image](https://user-images.githubusercontent.com/83301821/127878643-41858294-1680-4eae-8483-903d382bfe7c.png)

Above, a example of stateFullSet operation with use of PVC(we will explain in the next topics). In this case, a example of scale down and after scale up.

- Job

A Job creates one or more Pods and will continue to retry execution of the Pods until a specified number of them successfully terminate.

![image](https://user-images.githubusercontent.com/83301821/127882769-57a5eb9c-3078-4c79-9e8b-88930311f9e6.png)

- Cronjob

It also implements a job, but a schedule is done through a scheduler option (the syntax is the same as crontab)

Example:

![image](https://user-images.githubusercontent.com/83301821/127888364-2e33a406-8277-43b0-a547-ae4b9f30a651.png)

Note:

![image](https://user-images.githubusercontent.com/83301821/127888412-989c0b30-ab29-4963-b094-8963bd73b3ca.png)


- Service
An abstract way to expose an application running on a set of Pods as a network service.
With Kubernetes you don't need to modify your application to use an unfamiliar service discovery mechanism. Kubernetes gives Pods their own IP addresses and a single DNS name for a set of Pods, and can load-balance across them.

![image](https://user-images.githubusercontent.com/83301821/127695246-c4fb1cff-a9f2-4bb2-90bf-cfe188b0fc00.png)

In the above example, we expose a http nginx application in port 30001.

- Ingress

 Ingress exposes HTTP and HTTPS routes from outside the cluster to services within the cluster. Traffic routing is controlled by rules defined on the Ingress resource.
 
![image](https://user-images.githubusercontent.com/83301821/127892507-edfa6cff-f8f5-4a44-bd9c-54caeae710b0.png)

- ConfigMap

A ConfigMap is an API object used to store non-confidential data in key-value pairs. Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume.

Example:
(i) Creating a confimap type object:

![image](https://user-images.githubusercontent.com/83301821/127893122-0232071d-45c6-4166-81b5-c71b356cb034.png)

(ii) Associating a configmap value to pod :

![image](https://user-images.githubusercontent.com/83301821/127893251-d8694088-7a42-4bfe-89ba-55ded2302641.png)

- Secret

A Secret is an object that contains a small amount of sensitive data such as a password, a token, or a key. Such information might otherwise be put in a Pod specification or in a container image. Using a Secret means that you don't need to include confidential data in your application code.

![image](https://user-images.githubusercontent.com/83301821/127897578-0d363abd-766a-4a82-b19d-2de0bd7c00fb.png)

- Volume

As we've already mentioned, pod's are ephemeral. That is, if we try to store persistent data only with the pod's we will end up losing our data. It is in this sense that the use of volumes arises.
Differently from what we saw in docker, there are several types of volume of kubernetes in which each type is used for its due situation and for each pod we can define the desired amount as needed.

Bellow, the example:

![image](https://user-images.githubusercontent.com/83301821/127909751-f162dca0-df57-4a17-8f3e-7f3d2f6be1da.png)

- PV

A PersistentVolume (PV) is a piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using Storage Classes. It is a resource in the cluster just like a node is a cluster resource. PVs are volume plugins like Volumes, but have a lifecycle independent of any individual Pod that uses the PV. This API object captures the details of the implementation of the storage, be that NFS, iSCSI, or a cloud-provider-specific storage system.

- PVC
A PersistentVolumeClaim (PVC) is a request for storage by a user. It is similar to a Pod. Pods consume node resources and PVCs consume PV resources. Pods can request specific levels of resources (CPU and Memory). Claims can request specific size and access modes

# What are Custom Resource Definitions


