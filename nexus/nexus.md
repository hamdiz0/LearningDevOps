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

# `repo types` :

## `proxy repo` :

	* a repo that is linked to a remote one (maven-central)
	* nexus will check if the needed artifact is cached locally if not it will redirect the request to a remote repo and stored it locally and this will save time 

## `hosted repo` :

	* a private internal repo owned by a company

## `group repo` :

	* a combination of hosted and proxy repos in a single URL making it easier to manage access to multiple repos at once

# `creatinng a repo` :

	* admin conf => repository => repository => add repo based on the desired format and type

# `creating an authorized user` :

	* you can add users from the company system and configure acces permessions using the LDAP nexus integration 
	* admin conf => users => create user 
	* roles are needed to provide the minimum amount of permissions needed for a certain task
	* admin conf => security => roles => create role
	* privelige format : 
		- nx-repository-<View | Admin (for admin preveliges)>-<repo name>-<Central | Public | Snapshot | Release>-<* (all preveliges) ,delete ,edit ,read>
	* admin preveliges are usually for the admins of nexus hwo take care of backups and plugins in nexus
	* normal user are usaully devs hwo want to upload or retrieve artifacts
	* "View" preveliges are enuf for uploading and retrieving nexus repos
	* it make sense to only give "Snapshot" priveliges to normal user as they can deploy thier unstable releases
		- nx-repository-view-maven2-maven-snapshots-*
	* the created role is now assinable to any user

# `uploading jar files to nexus (maven & gradle) ` :

	* uploading a jar file to an existing repo on nexus requires configuring "Nexus Repo URL" and "Credentials" 
	* not the credantials of the admin but rather the users that have upload permissions
	* after creating an authorized user ,configs must be added to the "build.gradle" :
		- apply plugin: 'maven-publish'
		- publishing { (what to publish)
			publications {
				maven(MavenPublication){
					artifact("build/libs/my-app-$version"+".jar"){
						extention 'jar'
					}
				}
			}
			repositories { (where to publish)
				maven { 
					name 'nexus'
					url "http://<nexus ip>:<nexus port>/<path to repo>"
						"http://192.168.1.16:8081/repository/maven-snapshots/"
					credentials {
						username XXX
						password XXX
					}
				}
			}
		}
	* user name and password must be added to a "gradle.proprities" file not directly in the "build.gradle" file (checked into version control) 
	* gradle.proprities :
		- repo-user = <user name>
		- repo-password = <password>