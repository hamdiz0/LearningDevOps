# `jenkins` :

    * jenkins is a popular tool used for build automation and continious integration
<img src="img/jen1.PNG" width="100%">

# `build automation` :

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

# `CI/CD` :

    * CI/CD is the process of automating the whole software release cycle :
        - continious integrattion (CI) : new code changes are continuously built ,tested and merged 
        - continious deployment (CD) : automating further stages of the pipline ,automaticly deploying to different deployment environments including releasing production
    
<img src="img/jen2.PNG" width="100%">

# `setting up jenkins` :

    * it's better to set up jenkins as a docker container in a server :
        - docker run -v /home/hamdi/jenkins:/var/jenkins_home -p 8080:8080 -p 50000:50000 -u root jenkins/jenkins (-u:user ,-v:volume mapping ,-p:port mapping ,port 50000 is where jenkins master and the working nodes communicate)
        - docker exec -it <container name|id> bash (open a bash session inside the container)
