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
    * u can run oss on containers as long as they are based on the same kernel as the hosting machine (win containers cant run on a linux infrustructure)

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

    - docker run <image name> (run an instance "container" of an image "if the image dosen't exist localy it will be pulled from Docker Hub")
    - docker stop <container name|id>
    - docker rm <container name|id> (delete stoped or a running container)
        - docker rm <id1> <id3> <name4> (specifie multiple containers)
    - docker rm -v -f $(docker ps -qa) (remove all containers)

# `show exited & running containers` :

    - docker ps (show current running containers)
    - docker ps -a (show all containers "running & stoped") 

# `pull or remove an image` :

    - docker pull <image name> from Docker Hub"
    - docker rmi <image name> 
    - docker images (show current installed images)
        * all runnig instances "containers" of the image must be removed first

                            [`Docker Run`]

 * containers run under a docker host

# `Run-names` :

    - docker run --name=<custom name> <image name> (spcifie container name)

# `append & exec a command` :

    - docker run <image name>(ubuntu) <command>
        - docker run -it centos bash (create and enter a centos bash)
    - docker run ubuntu sleep 100 seconds (u can run other commands in this 100s periode)
        - docker exec <container name|id> <command> (append a command to a specified container)
        - docker exec -it <container name|id> bash 

# `Run-stdin` :

    - docker run -i <image name> (run in interactive mode)
        * this will make the container listen to inputs
        * add "-t" to attach a terminal (this will print prompts) 

# `Run - attach & detach` :

    * containers run in attached mode (wont let u interact with shell unless u force stop it Crtl+c)
    - docker run -d <image name> (run a container in detached mode or in background)
        -docker attach <container name|id> (run a container in the foreground )

# `Run-tags` :

    * tags specifie the image version ,by default the tag is specified as latest
    - docker run <image name>:<tag>
        - docker run redis:4.0

# `Run-PORT mapping|publishing` :  

    * a web-app (cantainer) with an ip@ on port 5000 can be accessed via the docker host with an ip@ on port 80 (5000 <=> 80)
    - docker run -p <doker host port>:<container port> <image name> 
        - docker run -p 80:5000 hamdi/web-app
        * now a user can access this web-app using "http://docker-host-ip@:80"

# `Run-Volume mapping` :

    * deleting a database container may result in the loss of all its data 
    * volume mapping allows backing up container data under the docker host
    - docker run -v <docker host dir>:<container dir> <image name> 
        - docker run /opt/data:/var/lib/mysql mysql
        - docker run -v /home/hamdi/jenkins:/var/jenkins_home -u root jenkins/jenkins

# `inspecting containers details & logs` : 

    - docker inspect <container name|id> (show container details)
    - docker logs <container name|id> (show conatiner log)

                            [`CREATING IMAGES`]

# `steps of creating a docker image` :

    * example of setting up a web app based on flask :
        - OS (ubuntu)
        - update apt repo
        - install dependencies using apt
        - install python dependencies
        - copy source code to /opt dir
        - run the web server using "flask" command
    * a docker file is needed to complete these steps :
    * "INSTRUCTION" => "argument"
    * it follows a layered architecture (OS => dependencys and tools => source-code => entrypoint)
        - Dockerfile contents :

            FROM Ubuntu

            RUN apt-get update
            RUN apt-get install python3
            RUN pip install python3-flask

            COPY app.py /opt/source-code (copy the app source-code to /opt)
            ENTRYPOINT python3 /opt/source-code (this command will run if a container is created)

# `create docker image `:

    - docker build Dockerfile -t(tag) <account name/web-app>

# `publish a docker image `:
    
    * it's necessary to login to ur account first 
        - docker login
    - docker push <account name/webapp>

# `chek image history` :

    - docker history <image name> 

# `failure & cached layers` :

    * docker image layers are cached (the build will continue from the last failed layer)
    * this helpfull when changing the source-code frequintly (lower layers are cached no need to rebuilt only the above layers need to)

                            [`ENVIRONMENT VARIABLES`]

# `setting up environment vars` :

    * env vars allow adding changes without modifying the source-code
    * it allow modifying the container form outside(host)
    * ur source-code have to read the env var in order to apply changes :
        * in pyhton :
            - import os
            - "var"=os.eniron.get("env var name")
        * js :
            - const "var"=process.env."env var name"
    - docker run -e <environment variable> <image name> (this will set up an env var inside the container's OS)
        - docker run -e BG_COLOR=blue hamdiz0/web-app

# `show container's env vars` :
    * env vars can be found under "Env" in the container config :
        - docker inspect <container name|id>

                            [`COMMANDS & ENTRYPOINTS`]     

# `Commands` :
    * it's posiible to pass in commands when running a container :
        -docker run <image name> <command>
            - docker ubuntu sleep 5
    * it's possible to make these permenet inside a container by modifing the image (Dockerfile ,both forms are valid) :
        - CMD sleep 5 
        - CMD [<command>,<parameter>] (json format)

# `Entrypoints` :

    * it will run a command when a container is created :
        - ENTRYPOINT ["command with out parameters"] (json format)
        - docker run <image name> <parameter>
            -docker run lazy-ubuntu 60
 
# `missing operand` :

    * this issue will happen when u don't specifie the parameter :
        - docker run lazy-ubuntu "missing parameter"
    * to fix this ,a combination of Entrypoints & Commands is needed (NOITCE:they must be specified in a json format ["cmd|param"]) :
        - ENTRYPOINT ["sleep"]
        - CMD ["60"]

# `overriding Entrypoints` :

    * it's possibel to override during container runtime :
        - docker run --etrypoint <command> <image name> <parameter>
            - docker run --entrypoint sleep2.0 lazy-ubuntu 60

                            [`DOCKER COMPOSE`] 

* Docker Compose is usefull for setting up porjects with multiple services (containers)

# `setting up docker compose` :

    * create a docker-compose.yml to manage multiple services and specific options needed in one file wish is easier to implement ,run and maintain
    * this is only possible on a single docker host

# `voting app` :

    * this helps understanding app-stack
    |voting-app(Python)|                    |result-app(Node.js)|
            ||                                       /\   
            \/                                       ||
    |in-memory-db(Redis)| => |worker(.NET)| => |db(PostgreSQL)|      

    * creating this app using doker run (naming containers is important):
        - docker run -d --name=redis redis
        - docker run -d --name=db db
        - docker run -d --name=vote -p 5000:80 voting-app
        - docker run -d --name=result -p 5001:80 result-app
        - docker run -d --name=worker worker
    * after running all of these containers ,links must be established for this to work (voting-app needs to recognize the redis db for example):
        - docker run --link <image name of the container u want to link>:<container name> <image name> 
            - docker run -d --name=vote -p 5000:80 --link redis:redis voting-app (this will create an entry in /etc/hosts of the voting's app container "ip@ redis")
            - docker run -d --name=result -p 5001:80 --link db:db result-app
            - docker run -d --name=worker --link redis:redis --link db:db worker
    * creating this app using docker compose :
        - docker-compose.yml :
            redis:
                image: redis
            db:
                image: db
            vote:
                image: voting-app
                ports:
                    - 5000:80
                links:
                    - redis
            result:
                image: result-app
                ports:
                    - 5001:80
                links:
                    - db
            worker:
                image: worker
                links:
                    - redis
                    - db
            
# `run the app stack (yml file)` :

    - docker-compose up (bring the entire application stack)

# `docker compose build` :
    
    * docker compose build allow building an application stack when some services or parts are not completely developed yet
    * to accoplish this the "image" attribute must be swaped with "build" :
        - docker-compose.yml :
            vote:                 => vote:
                image: voting-app        build: ./vote
        * "./vote" containes source-code (development in progress) and a docker file with instructions to build the docker image

# `docker compose versions` :
    
    * version 1 : (creating this app using docker compose)
    * version 2 : same as version 1 but all of the services must be under a proprity named "services" and the version must be specified 
    * version 2 will eleminate the need for links as it sets up a bridged connection between services automaticly 
        - docker-compose file :
            version: 2
            services:
                same code as version 1 but without the links part
        * to set dependencys between certain services u can add "depends_on" attribute :
            - docker-compose file :
                vote:
                    depends_on:
                        - redis 
    version 3 : same as version 2 with removed and added features and it has "docker swarm"

# `docker compose networks` :

        * say if we want to split these services into two networks "back-end" and "front-end"
        - docker-compose file :
            version: 2
            services:
                redis:
                    image: redis
                    networks: 
                        - back-end
                db:
                    image: db
                    networks: 
                        - back-end
                vote:
                    image: voting-app
                    networks: 
                        - back-end
                        - front-end
                ...
            networks:
                - back-end:
                - front-end: 

                            [`DOCKER REGISTRY`]