# `nexus` :
	
	* nexus is an artifact repo manager

## `artifacts` :

	* artifacts are apps built into a single file (multiple app source code in one file)
	* an artifact may have multiple formats : jar ,zip ,tar ,...

## `artifact repo manager` :

	* this is where you store or upload artifcats as long as it supports the artifact file format
	* each format has its own repo (nexus supports multiple formats)
	* you can also retrieve stored artifacts (a centrale storage) 
	* you can host youre own repos (private) ,set up proxy repos (retrieve public repos and acces artifacts from nexus)
	* it's best practice to manage all artifact repos in one spot and nexus provides that

## `features of nexus` :

	* integration with "LDAP" : configure access manegement and permissions
	* flexible and powerfull "REST" api for integration with other tools (like jenkins and gitlab) so basicly its an essantial part in the CI/CD pipline 
	* push artifacts (jenkins) to nexus than pull and deploy to a deployment server

<img src="img/nex1.PNG" width="100%">
	
	* back up and restore features that manages storage and artifact load
	* multi-format support

<img src="img/nex2.PNG" width="100%">

	* metadata tagging (label and tag artifact realeases like dev or release versions)
	* cleanup policies (remove old uneeded artifacts and save space) ,this can be automated (weekly ,monthly)
	* search functionality across projects and artifact repos to retrieve the desired version 
	* user token support (non human user authentication) wich helps with integration in the CI/CD pipline

# `setting up nexus` :
	
	* download tar file from "https://sonatype-download.global.ssl.fastly.net/repository/downloads-prod-group/3/nexus-3.72.0-04-unix.tar.gz"
		- wget <url>
	* untar the file :
		- tar -zxvf <tar file>
	* it's better to set a nexus user that manages the nexus data :
		- useradd nexus 
	* change the "nexus-version" and "sonatype-work" folders ownership with thier content :
		- chown -R (recursive) nexus:nexus nexus-version
		- chown -R nexus:nexus sonatype-work
	* java must be installed on the machine :
		- apt install openjdk-17-jdk openjdk-17-jre
	* start nexus :
		- nexus-version/bin/nexus start
		- ps aux | grep nexus (check nexus is running)
	* display info about listening network services :
		- netstat -lnpt
	* nexus service is listening on port 8081 ,nexus hosting server must be configured to allow in/outbound port 8081 traffic
