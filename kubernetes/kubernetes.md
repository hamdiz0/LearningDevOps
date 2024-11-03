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

* `kube-api-server`:
    - Exposes the Kubernetes API
    - Front-end for the Kubernetes control plane
    - All communication in the cluster utilizes this API
    - Designed to scale horizontally and balance traffic
* `etcd` :
    - Highly available, distributed key-value store that contains all cluster data
    - Stores deployment ,configuration data ,the desired state and meta data 
* `schduler` :
    - Assigns newly created Pods to nodes
    - Selects optimal node according to Kubernetes scheduling principles, configuration options, and available resources
* `kube-controller-manager` :
    - Monitor cluster state
    - Ensure the actual state matches the desired state
* `cloud-controller-manager` :
    - Runs controllers that intreract with cloud providers
    - link clusters to a cloud provider's API 

---

<img src="img/kub5.PNG" style="width:100%">

* `nodes` :
    - Are the worker machines (virtual or physical) in Kubernetes
    - Managed by the control plane 
    - Contain the services necessary to run applications
    - Nodes include pods which are the smallest deployment entity in Kubernetes
* `pods` : 
    - pods include the working containers
* `kubelet` :
    - Communicates with the API server
    - Ensure that pods and their associated containers are running
    - Reports to the control plane on the pods' health and status
    - in order to start a pod the kubelet uses the contatiner runtime (docker)
* `contatienr runtime` :
    - Downloads images and runs contaitners
    - k8s implements an interface so that this componenet is pluggable
* `kube-proxy` :
    - Mantains network rules that allow communication to pods  
    - communication to workloads running in a cluster

# `k8s objects` :

* Kubernetes objects consist of two main fields 
    - object spec :
        * provided by user
        * defines desired state
    - status :
        * provided bu kubernetes
        * defines current state
    - kubernetes works towards matching the current state to the desired state
* Labels and Selectors :
    
    <img src="img/kub6.PNG" style="width:100%"> 
    
* `Namespaces and names` :
    - provide a mechanism for isolating groups of resources within a single cluster
    - segregate cluster by team ,project ,etc 
    - necessary with larger numbers or users

<img src="img/kub7.PNG" style="width:100%">

* `Pods` :
    - simplest unit in kubernetes 
    - represents processes running on a cluster
    - encapsulates one or more contaitners
    - replicating a pod serves to scale applications horizontally
    - example file.yml :
    ```
        apiVersion: v1
        kind: Pod
        metadata:
            name: nginx
        spec:
            containers:
            - name: nginx
              image: nginx:latest
              ports:
              - contatinerPort: 80
    ```
* `ReplicaSet` :
    - a set of horizontally scaled running Pods
    - it's configuration file defines:
        * Number of replicas 
        * Pod template
        * Selector to identify which Pods it can acquire
    - example file.yml :
    ```
        apiVersion: apps/v1 
        kind: ReplicaSet 
        metadata:
            name: nginx-replicaset 
            labels:
                app: nginx
        spec:
            replicas: 3 
            selector: // wich Pods to be acquired 
                matchLabels: 
                    app: nginx
            template: // Pod template
                metadata: 
                    labels:
                        app: nginx
                spec:
                    containers:
                        name: nginx
                        image: nginx:1.7.9 
                        ports:
                            containerPort: 80
    ```
    - Generally encapsulated by a Deployment
* `Deployment` :
    - a deployment is higher-level object that provides updates for Pods and ReplicaSets (a blueprint)
    - run multiple replicas of an application 
    - suitable for stateless applications
    - update triggers a rollout (a rolling update scales up a new version to the appropriate number of replicas and scales down the old version to 0 replicas)
    - file.yml example:
    ```
        apiVersion: apps/v1 
        kind: Deployment 
        metadata:
            name: nginx-deployment
            labels:
                app: nginx
        spec:
            replicas: 3 
            selector:
                matchLabels: 
                    app: nginx
            template: 
                metadata: 
                    labels:
                        app: nginx
                spec:
                    containers:
                        name: nginx
                        image: nginx:1.7.9 
                        ports:
                            containerPort: 80
    ```
* `Service` :
    - a REST object similar to Pods
    - a logical abstraction for a set of pods in a cluster
    - provide policies for accessing the Pods and cluster
    - acts as load balencer across the Pods (forwards request to the less busy Pod)
    - eash service is assigned a unique IP@ for accessing applications deployed on Pods
    - why service is needed :
        * Pods are volatile wich leads to discoverability issues because of changing IP@
        * services keep track of Pod changes and exposes a single IP@ or a DNS name
        * utilizes selectors to target a set of Pods
    - Service Types (4):
        * ClusterIP (internal) : 
            <img src="img/kub8.PNG" style="width:100%">

        * NodePort (external) :

            <img src="img/kub9.PNG" style="width:100%">

        * ELB (External Load Balancer) (external) :

            <img src="img/kub10.PNG" style="width:100%">

        * External name (external) :

            <img src="img/kub11.PNG" style="width:100%">

    - basicly a pod wrap with persisting settings
* `Ingress` :
    - forwards connection outside/inside the kube internal network
    
<img src="img/kub12.PNG" style="width:100%">

* `DaemonSet` :
    - adjust replica-number when adding/decreasing Nodes
    - ensure that Pods are equally distributed across deployments
    - deploys one replica per node

<img src="img/kub13.PNG" style="width:100%">

* `StatefulSet` :
    - used specificly for apllication like databases
    - basicly Deployment but for databas services
    - data bases are often hosted outside of the k8s cluster avoiding the StatefulSet

<img src="img/kub14.PNG" style="width:100%">

* `Job` :

<img src="img/kub15.PNG" style="width:100%">

* `Config Map` :
    - map external configuration to an application
    - connected to a Pod so that it can retrieve the configuration
    - avoid rebuilding ,pushing the image ,pulling in the pod evry time a change happens 
* `Secret` :
    - store credentials
    - require third party encryption tools (cloud providers, ...)
    - or reference secret inside deployment/pod (environment vars ,proprities file ".env")
* `volumes` :
    - persist data locally/remotely