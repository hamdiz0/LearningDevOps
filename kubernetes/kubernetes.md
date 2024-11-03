# Kubernetes

* kubernetes is a container orchestration tool
* automating deployment ,scaling and management of containerized apps

# `contatiner orchestration` :

* container orchestration is a process that automates the container lifecycle of containerized apps :
    - deployment
    - manegement
    - scaling
    - networking 
    - availability
* container orchestration is critical part of an organization's security ,orchestration, automation and response (SOAR) requirements

<img src="img/kub1.PNG" style="width:100%">

# `k8s concepts` :

<img src="img/kub2.PNG" style="width:100%">
<img src="img/kub3.PNG" style="width:100%">

# `k8s Architecture` :

<img src="img/kub4.PNG" style="width:100%">

* kube-api-server :
    - Exposes the Kubernetes API
    - Front-end for the Kubernetes control plane
    - All communication in the cluster utilizes this API
    - Designed to scale horizontally and balance traffic
* etcd :
    - Highly available, distributed key-value store that contains all cluster data
    - Stores deployment ,configuration data ,the desired state and meta data 
* shceduler :
    - Assigns newly created Pods to nodes
    - Selects optimal node according to Kubernetes scheduling principles, configuration options, and available resources
* kube-controller-manager :
    - Monitor cluster state
    - Ensure the actual state matches the desired state
* cloud-controller-manager :
    - Runs controllers that intreract with cloud providers
    - link clusters to a cloud provider's API 

<img src="img/kub5.PNG" style="width:100%">

* nodes :
    - Are the worker machines (virtual or physical) in Kubernetes
    - Managed by the control plane 
    - Contain the services necessary to run applications
    - Nodes include pods which are the smallest deployment entity in Kubernetes
* pods : 
    - pods include the working containers
* kubelet :
    - Communicates with the API server
    - Ensure that pods and their associated containers are running
    - Reports to the control plane on the pods' health and status
    - in order to start a pod the kubelet uses the contatiner runtime (docker)
* contatienr runtime :
    - Downloads images and runs contaitners
    - k8s implements an interface so that this componenet is pluggable
* kube-proxy :
    - Mantains network rules that allow communication to pods  
    - communication to workloads running in a cluster




