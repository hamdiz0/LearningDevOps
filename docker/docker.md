                            [`DOCKER`]
# `why Docker is needed` :

    * compatibility/dependency (all different services must be compatible "versions" on the same infrastructure "os")
    * some services may require different versions and libraries of the same dependency
    * long setup time (the project changes over time that requires updating dependency and changing the infrastructure "Matrix-Hell")
    * different Dev/Test/Prod environments (new develpers have to set up thier working environment form scratch wich is tedious)
    * the main purpose of Docker is to package ,contanerize applications ,ship them and run them anywhere   

# `containers` :

    * isolated environments (Processes,Network,Mounts)
    * some kind of virtual machines but all chare the same os kernel 
    * you can run each service on a seperate container with its dependecys and libraries
    * u can run oss on containers as long as they are based on the same kernel as the hosting machine (win containers cant run on a linus infrustructure)

# `difference between Containers & VM` :

    * Virtual Machine (Apps,Libs & Deps,OS) => Hypervisor => Hardware
    * Container(Apps,Libs & Deps) => Docker => OS => Hardware
    * Containers consume less resources unlike VMs
    * Containes & VMs work together (VMs provsion containers wich provisoin apps and scale them this allows of the support of large amount apps running on multiple Docker hosts)
    * Containers are not meant to host an OS ,their are meant to run a specific task or a process (web server ,data-base ,...)
    * once the container completes its task or the process inside of it ,it exits 
 
# `Docker images` :

    * a Docker image is a Package ,Template or Plan (service ,application)
    * containers are running instances of images wich have their own environments
    * create personal images and push it to "Docker Hub" repo
    * Docker images are found in Docker Hub "hub.docker.com"
    
                            [`SETTING UP DOCKER`]

* "docs.docker.com" => get Docker => select OS => follow the listed steps

# `Linux`:

    * installing docker using the convinience script is mush easier 
        - curl -fsSL https://get.docker.com -o get-docker.sh
        - sudo sh get-docker.sh --dry-run (show the script steps)
        - sudo sh get-docker.sh (run the script)

# `Windows` :
    -
                            [`COMMANDS`]

* higher priveliges are requierd to run docker commands

# `show version` :

    - sudo docker version

# `create ,stop or remove a container` :

    - docker run "image name" (run an instance "container" of an image "if the image dosen't exist localy it will be pulled from Docker Hub")
    - docker stop "container name|id"
    - docker rm "container name|id" (delete stoped or a running container)
        - docker rm "id1" "id3" "name4" (specifie multiple containers)
    - docker rm -v -f $(docker ps -qa) (remove all containers)

# `show exited & running containers` :

    - docker ps (show current running containers)
    - docker ps -a (show all containers "running & stoped") 

# `pull or remove an image` :

    - docker pull "image name from Docker Hub"
    - docker rmi "image name"
    - docker images (show current installed images)
        * all runnig instances "containers" of the image must be removed first

# `append & exec a command` :

    - docker run "image name(ubuntu)" "command"
        - docker run -it centos bash (create and enter a centos bash)
    - docker run ubuntu sleep 100 seconds (u can run other commands in this 100s periode)
        - docker exec "container name|id" "command" (append a command to a specified container)
        - docker exec -it "container name|id" bash 

# `run - attach& detach` :

    * containers run in attached mode (wont let u interact with shell unless u force stop it Crtl+c)
    - docker run -d "image name" (run a container in detached mode or in background)
        -docker attach "container name|id" (run a container in the foreground )

# `run-tags` :

    * tags specifie the image version ,by default the tag is specified as latest
    - docker run "image name":"tag"
        - docker run redis:4.0
         