# `jenkins` :

    * jenkins is a popular tool used for build automation and continious integration
![jen1](/jenkins/jen1.png)
# `setting up jenkins` :

    * it's better to set up jenkins as a docker container in a server :
        - docker run -v /home/hamdi/jenkins:/var/jenkins_home -p 8080:8080 -p 50000:50000 -u root jenkins/jenkins (-u:user ,-v:volume mapping ,-p:port mapping ,port 50000 is where jenkins master and the working nodes communicate)
        - docker exec -it <container name|id> bash (open a bash session inside the container)
