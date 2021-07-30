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
