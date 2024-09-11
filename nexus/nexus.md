# `nexus` :
	
	* nexus is an artifact repo manager

# `setting up nexus` :
	
	* download tar file from "https://sonatype-download.global.ssl.fastly.net/repository/downloads-prod-group/3/nexus-3.72.0-04-unix.tar.gz"
		- wget <url>
	* untar the file :
		- tar -zxvf <tar file>
	* it's better to set a nexus user that manages the nexus data :
		- useradd nexus 
	* change the "nexus-version" and "sonatype-work" folders ownership with thier contant :
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
