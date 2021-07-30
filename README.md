# ia_week4_k8s

- What is Kuberbenetes?

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
