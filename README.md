#                           What is DevOps ?

<img src="z-imgs/loop.jpg" style="width:100%">

## `devops is not` :

    - devops is not a tool 
    - not a separate team 
    - not just automation
    - not simply combining Dev and ops teams

    => devops is not just Dev and Ops working together while remaning in thier seperate silos

## `devops is` :

    - devops is based on agile priciples
    - devops is based on CI/CD
    - delevering software in a rapid continuous manner
    - Dev and Ops teams working togther not in seperate silos

    => devops is a "CULTURE CHANGE" in wich Dev and Ops engineers work together during the entire development cycle
    
    => devops is a methodology that integrates software development (Dev) and IT operations (Ops) to improve collaboration, accelerate software delivery, and ensure more reliable system 

#                           [`When to use DevOps ?`]

## `when` :

    - rapid and Frequent Releases (frequent and rapid updates)
    - collaboration and Communication Issues (devops breaks silos and improve collaboration)
    - scalability and Growth (devops work well with cloud-based environment ,automated infrastructure and CI/CD ...)
    - continuous Feedback and Improvement (user feedback helps)
    - complex Systems with High Availability (mission-critical systems where uptime and reliability are essential)
    - microservices Architecture

## `when not` :

    - small, static projects
    - heavily regulated industries with slow change (goverment or medical fields)
    - Legacy Systems with Monolithic Architecture

#                           [`Software Development Roles`]

    - there are different roles in software development & delevery process

## `software development` :

    - software programmed by devs using different programming languages
    - add new features and bug fixes

## `software testing` :

    - test new features and old functionality
    - manual and automated testing
    - done by testers

## `operations (software release)` :

    - build application
    - deploy on servers
    - upgrade existing software
    - done by opertions team

#                            [`traditional : development vs operatons`]

    - different responsabilities
    - different technical knowledge
    - different toolsets

## `development` :

    - focus on implementing  new features fast
        - programming languages
        - test framworks
        - databases
        - version control

## `operations` :

    - focus on maintaining stability
        - os
        - command line
        - scripting
        - monitoring tools

## `this seperation between the development and operation team causes multiple issues` :

    - "well it works on my machine !!!"
    - different responsibilities , different technical knowledge and different tools  
    - this will slow down the release process (weeks to months)

### `misscommunication and lack of collaboration ` :

    - deployment requires configuration and environment needs to be prepared
    - dev team give instructions to the ops team ,these instructions may not be clear enough or some parts are missing

### `conflict of intrest` :

    - DEV focus on realising new features
    - OPS focus on maintaining stability 

### `manual work and checklist` :

    - manual checks : are the system stability and security affected by the new changes 
    - manual deployment
    - manual configuration

#                            [`solution DevOps`]

## `defenition` :

    - devops is the intersection of DEV and OPS
    - a common language to ensure the communication between devs and ops team
    - devops is all about making the process of continious delivery fast and with minimal errors
    - it tries to remove all these roadblocks and things that slow down the release process
    - it helps create fully streamlined automated process for release cycles

## `devops as a seperate role` :

    - devops become an acual role : "devops engineer"
    - devops tools : set of technologies used to implement devops
    - a devops engineer is responsible for creating a streamlined fully automated release process
    - basic knowledge of the development and operation and additional devops specific skills

## `famous devops tools` :

<img src="z-imgs/loop & tools.jpg" style="width:100%">

    - source code manegment : git
    - package management : docker
    - infratructure as code : terraform ,ansible
    - CI/CD : jenkins ,git web service
    - container orchestration : kubernetes
    - cloud : aws ,azure ,google cloud
    - monitoring : prometheus

#                            [`waterfall vs agile methedologie`]

## `waterfall` :

    - requirements : planning
    - development : code complete app
    - testing : testing the hole app
    - operations : huge preparation
    => this an ineffective process :
        - over time new requirements may arise
        - miscommunication and places of faliure
        - lack of fast feedback

## `agile` :

    - agile is the heart of CI/CD process
    - devops implements some best practices of the agile method
    - backlog => analyse => define => design => test => deploy
    => this method is effective and its increasingly growing :
        - speed of development , testing and deployment cycles
        - each feature gets tested , deployed and gets immediate feedback
        - fast development and deployment process
        - scrum and kanban (examples of specific implementations)
    

#                            [`at the core of devops`]

    - CI/CD pipline for an automated release process
    - commit code => test => build => push => deploy
