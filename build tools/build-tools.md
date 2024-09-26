#                           [`BUILD TOOLS`]

# `artifacts` :

    * apps need to be deployed on a production server 
    * application code and its dependencies must be packaged into a single movable file called an artifcat wich's esier to deploy on servers 
    * building the code / packaging :
        - compile the code
        - compress into a single file
    * the artifact can be deployed on multiple servers like development ,test and production so there should be a back up in case of failure ,so artifacts must be stored on an artifact repository like nexus
    * an artifact can have a specific format/extention depending on the programming lanuage used :
        - java => .jar or .war 
        - python => .pyz or .whl
        - nodejs => .zip or .tar

# `settings up build tools` :

## `linux` :

    * java :
		- apt install openjdk-<version> (17)-jdk
	* SDK to install gradle :
		- curl -s "https://get.sdkman.io" | bash
		- source "$HOME/.sdkman/bin/sdkman-init.sh"
		- sdk install gradle <version> (7.4)
    * maven :
        - apt install maven
    * nodejs && npm :
        - apt install nodejs npm

## `win` :

    * downlowd java <version> ,maven and gradle 
    * edit the system environment variables => environmeent variables under advanced tab 
    * add java ,maven and gradle paths inside the "path" variable (double click)
    * add "JAVA_HOME" along with th "path" variable in the system variable section
    * for nodejs & npm download the installer from official website 

# `basic commands` :

## `maven & gradle` :

    * maven :
        - mvn archetype:generate \
        > -DgroupId=com.example -DartifactId=<name> \ 
        > -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
        - mvn clean install|package (in the project folder to build it)
        * basic structure :  
            my-app
            ├── pom.xml
            └── src
                ├── main
                │   └── java
                │       └── com
                │           └── example
                │               └── App.java
                └── test
                    └── java
                        └── com
                            └── example
                                └── AppTest.java
    * gradle :
        - gradle init
        - gradle build
        * basic structure :
            my-app
            ├── build.gradle
            ├── settings.gradle
            └── src
                ├── main
                │   └── java
                │       └── com
                │           └── example
                │               └── App.java
                └── test
                    └── java
                        └── com
                            └── example
                                └── AppTest.java

## `npm` :
    
    * start basic project :
        - npm init -y 
    * you can start with popular templates :
        - npx create-react-app my-app
    * install needed dependencies :
        - npm install (installs dependencies found in the package.json)
        - npm install <dependencie> --save (install a dependencie and add it to the package.jso file)
    * basic structure :
        my-app
        ├── package.json
        ├── index.js
        └── test
            └── test.js



