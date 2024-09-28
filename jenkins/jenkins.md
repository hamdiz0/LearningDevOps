#                             [`JENKINS`]

    * jenkins is a popular tool used for build automation and continious integration

## `use of jenkins` :

    * jenkins is prefarable to be installed on a server
    * it require's needed tools to get the task done (docker ,npm ,...)
    * tasks must be configured (run tests ,build app)
    * configuration of the automatic trigger of the workflow
    - run tests
    - build ,publish and deploy artifacts
    - send notifications and more

## `roles in jenkins` :

### `jenkins administrator (operation or devops teams)` :

    - manges jenkins
    - sets up jenkins cluster
    - install plugins 
    - backup jenkins

### `jenkins user (devloper or devops teams)` :

    - create actual jobs to run workflows (automate apps workflow)

<img src="img/jen1.PNG" width="100%" height="500px">

#                             [`Build Automation`]

    * is the process of automating :
        - getting the source code 
        - executing automated tests 
        - compiling into binary code/build docker image
        - push artifact to repository
        - deploy artifact
    => the proess of doing this manually is not convinient :
        - stash working changes and move to main branch
        - login to the correct docker repo
        - execute tests (can't code in this step)
        - build doker image and push to repo
    * to automate this it is preferable to have a dedicated server executing these tasks automaticly :
        - preparing test environment
        - docker credentials configured
        - all necessary tools installed
        - trigger the build automaticly

#                             [`CI/CD`]

    * CI/CD is the process of automating the whole software release cycle :
        - continious integrattion (CI) : new code changes are continuously built ,tested and merged 
        - continious deployment (CD) : automating further stages of the pipline ,automaticly deploying to different deployment environments including releasing production
    
<img src="img/jen2.PNG" width="100%" height="200px">

#                             [`Setting up Jenkins`]

    * it's better to set up jenkins as a docker container in a server :
        - docker run -v /home/hamdi/jenkins:/var/jenkins_home -p 8080:8080 -p 50000:50000 -u root jenkins/jenkins (-u:user ,-v:volume mapping ,-p:port mapping ,port 50000 is where jenkins master and the working nodes communicate)
        - docker exec -it <container name|id> bash (open a bash session inside the container)

#                             [`Plugins and Tools`]

    * you can add tools and plugins from the jenkins ui under the manage/administer tab :
        - you need download the plugin from the plugin tab (avaible plugins) first then installed in the tools tab 
    * it's also possible with shell commands in the jenkins container :
        - docker exec -it <jenkins container name|id > <bash>

#                             [`Job Types`]

## `freestyle` :

    - the most basic job type ,it's straightforward to set up and configure
    - suitable for simple projects
    - lack some advanced features

## `pipline` :
    
    - orchestrates long-running avtivities that can spam multiple build agents
    - suitable for building piplines/workflows and/or organizing complex avtivities

## `multibranch pipline` :

    - creates a set of pipline projects according to detected branches in one SCM repo (Source code management is used to track modifications to a source code repository)

#                             [`Setting Up a Job`]

    * choose job type
    * job => configure => build environment => build steps => command: you can execute shell commands as long as these tools are installed using shell in the container (commands of tools installed from the ui won't work)
    * there is an option that allows executing commands from tools and plugins
    "add build step" => choose plugin and wirite a related command
    * installing directly on the server (container) is more flexible unlike plugins that provides limited input fields
    * you can build the job by selecting "build now"
    * see build status in the "status" tab
    * and other options like delete and see changes

#                             [`Git Configuration`] 

    * job => configure => source code manegement : you can select the "git" option to sync a project repo
    * credentials must be added in order to acces the git repo : select "add" under credentials and add user name and password of the git repo*
    * it's also possible to select a specific branch if a repo containes  multiple

<img src="img/jen3.PNG" width="100%" height="400px">
    
    * jenkins checks out the source code locally in order to be able to run commands against the git repo like tests
    * build option will build the application locally
    * jenkins config files can be found under "/var/jenkins_home/" (jenkins container shell)
    * you can find all created jobs with their information (log files ,builds) under the "jobs" dir 
    * the "git checkout" is under "/var/jenkins_home/workspace/<job name>" (you will find the actual repo source code)

#                             [`Scripts`]

    * jenkins can run sript files located in a synced git repo 
    * job => configure => build environment => build steps => command :
        - chmod +x <script> (needed execute permissions)
        - ./<script>

#                             [`Run Tests and Build a Java App`]

    * example of retriving a java-maven app from a git repo ,run test and build a jar file   

<img src="img/jen4.PNG" width="100%" height="400px">

    * sync repo with credentials "https://gitlab.com/hamdiz0/java-maven-app.git" (branch:jenkins jobs)

<img src="img/jen5-git repo.PNG" width="100%" height="400px">

    * job => configure => build environment => build steps => add build step : choose maven : 
        - goals : test (test app)
        - goals (add a second step) : package (package to jar file)

<img src="img/jen6 mvn test-package.PNG" width="100%" height="400px">

    * jenkins will checkout the git repo first ,run tests than package the app into a jar file (dependencies will be installed in the process)
    * a "target" folder is created containing the jar file


#                             [`Doker in Jenkins`]

## `setting up docker in jenkins` :

    * adding docker by attaching a volume to jenkins from the host 
    * this achievd by mounting the docker runtime dir "/var/run/docker.sock" of the host to the jenkins container as a volume (previous container must be killed to add volumes) :
        - docker run -v /home/hamdi/jenkins:/var/jenkins_home \
        > -v /var/run/docker.sock:/var/run/docker.sock \
        > -p 8080:8080 -p 50000:50000 \
        > -u root jenkins/jenkins
    * additional steps are needed (commands inside the jenkins container) : 
        - curl https://get.docker.com/ > dockerinstall && chmod 777 dockerinstall && ./dockerinstall
        - chmod 666 /var/run/docker.sock

## `build & push docker images` :

    * build a docker image of the "java-maven-app" :
        - docker build . -t hamdiz0/java-maven-app 
    * to push a docker image to a docker repo credentials must be added 
        * manage => credentials => store/system (of the related git repo credentials) => global credentials(unrestricted) => add credential

<img src="img/jen9.PNG" width="100%" height="400px">

    * a plugin is needed to provide the user name and password of docker 
        * build environment => use secret text(s) or file(s) => username and password (seperated) => set user name (USER) and password (PASSWORD) variables

<img src="img/jen7.PNG" width="100%" height="400px">

        - docker login -u $USER -p $PASSWORD
            - echo $PASSWORD | docker login -u USER --password-stdin (best practice)
        - docker push hamdiz0/java-maven-app

<img src="img/jen8 custom sctipt.PNG" width="100%" height="400px">

    * in order to push from jenkins to the nexus docker repo it must be secured first 
    * in the jenkins host where docker is installed (container or host where the actual docker installation exists) edit /etc/docker/docker.json :
    - {
        "insecure-registries": ["<nexus-ip@>:<port>"]
      } 
        - {
            "insecure-registries": ["192.168.1.16:8082"]
          }
    * check connection :
        docker login 192.168.1.16:8082
    * restart docker to add changes :
        - systemctl restart docker
        - chmod 666 /var/run/docker.sock (redo essantial changes after restart) 
    * add nexus credentials in jenkins (nexus user must have docker role permissions)
    * modify the script :
        docker build . -t <nexus-ip@>:<docker repo http port>/java-maven-app:1.1
        echo $PASSWORD | docker login -u $USER --password-stdin   <nexus-ip@>:<docker repo http port>
        docker push <nexus-ip@>:<docker repo http port>/java-maven-app:1.1
<img src="img/jen10.PNG" width="100%" height="400px">   

