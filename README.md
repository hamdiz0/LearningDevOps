# `DevOps` :
    - there are different it roles in software development & delevery process
## `software development` :
    - software programmed by devs using different programming languages
    - add new features and bug fixes
## `software testing` :
    - test new features and old functionality
    - manual and automated testing
    - done by testers
## `operations` :
    - build application
    - deploy on servers
    - upgrade existing software
    - done by opertions team
# `traditional : development vs operatons` :
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
    - this will slow down the release process
### `misscommunication and lack of collaboration ` :
    - deployment requires configuration and environment needs to be prepared
### `conflict of intrest` :
    - DEV focus on realising new features
    - OPS focus on maintaining stability 
### `manual work and checklist` :
    - manual checks : are the system stability and security affected by the new changes 
    - manual deployment
    - manual configuration
# `solution DevOps` :
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
    - source code manegment : git
    - package management : docker
    - infratructure as code : terraform ,ansible
    - CI/CD : jenkins ,git web service
    - container orchestration : kubernetes
    - cloud : aws ,azure ,google cloud
    - monitoring : prometheus
# `at the core of devops` :
    - CI/CD pipline for an automated release process
    - commit code => test => build => push => deploy
