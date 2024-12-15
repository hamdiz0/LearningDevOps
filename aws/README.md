# AWS

# [`What is the Cloud ?`]

* Cloud computing delivers IT resources over the internet on a pay-as-you-go basis, allowing companies to avoid owning hardware and physical infrastructure.

* Cloud computing reduces costs, boosts flexibility, and simplifies operations

## `AWS and the cloud` :

AWS provides these services, enabling businesses to run applications without managing servers or physical data centers, saving time and focusing on core business needs.

## `6 key benefits` :

* Pay only when you use resources.
* Lower costs due to shared demand.
* No capacity planning—scale as needed.
* Quick setup—provision in minutes.
* Skip data center upkeep—focus on what matters.
* Global reach in a few clicks.

# [`Global Infrustructure?`]

<img src="img/aws2.PNG" style="width:100%">

* AWS regions are geographic areas that contain multiple availability zones
* availability zones cantaines data centers
* edge locations and rigional edge caches used to cache data closer to end users this reduces latency
* choosing an aws region :
    - latency
    - price
    - service availability
    - data compliance/regulations (storing user data in a specifc location)

# [`Security on AWS`]

* both aws and the customer are responsible for the security (aws shared responsability)

<img src="img/aws3.PNG" style="width:100%">

## ` security of the cloud (aws)` :

* aws is required to protect and secure the infrastructure that runs all the services 
* aws classifies the level of responsibility of services into three different categories

<img src="img/aws4.PNG" style="width:100%">

## ` security in the cloud (customer)` :

* the customer is responsible for configuring services and securing data. 
* the level of responsibility varies based on the type of aws service

<img src="img/aws5.PNG" style="width:100%">

* it's important to know your security responsibilities for each service and make sure they match your IT security rules and legal requirements :
    - choosing the right region: pick a location that meets local data laws
    - protecting data: use encryption and create backups
    - controlling access: limit who can access your data and resources

# [`IAM`]

* IAM (Identity and Access Management) is an AWS tool to control access to your account and resources. It lets you manage who can access AWS resources (authentication) and what they can do (authorization)

<img src="img/aws6.PNG" style="width:100%">

* IAM Users and Groups : 
    - IAM Users: Individuals or applications that access AWS. Each user has unique credentials.
    - IAM Groups: A collection of users with the same permissions, making it easy to manage access. For example, developers, admins, and security roles can be grouped to control permissions.
* IAM Policies :
    - rules that specify what users, groups, or roles can and cannot do in AWS 
    - JSON format that contains four elements :
        - version
        - effect Allow/Deny
        - action specify permitted or denied actions
        - resources the policy applies to
* admin ploicy :
```
    {
        "Version": "2012-10-17",
        "Statement": [
            {
            "Effect": "Allow",
            "Action": "*",
            "Resource": "*"
            }
        ]
    }
```
* limited access policy :
```
    {
        "Version": "2012-10-17",
        "Statement": [
            {
            "Effect": "Allow",
            "Action": [
                "iam:ChangePassword",
                "iam:GetUser"
            ],
            "Resource": "arn:aws:iam::123456789012:user/${aws:username}"
            }
        ]
    }
```
* IAM roles :
    - using roles in IAM is simpler and more secure than managing individual user accounts
    - Temporary Credentials: When you assume a role, IAM gives you temporary access keys that automatically expire after a set short time 
    - Long-Term Credentials: Users have permanent credentials ,which remain active until you enforce a password policy for regular updates.

<img src="img/aws7.PNG" style="width:100%">

* steps :
    * create an IAM role
    * attach the role to EC2
    * update web app code
    * the app makes API calls using temporarly credentials

<img src="img/aws8.PNG" style="width:100%">

* add a role in the IAM conf

<img src="img/aws9.PNG" style="width:100%">

* choose permissions for the role 
* a best practice is to not give full permission rules

<img src="img/aws10.PNG" style="width:100%">

* aws IAM Identity Center (IAM IC) lets employees sign in once to access all assigned aws accounts and apps in one place :
    - single login for all aws resources
    - syncs users from external identity providers
    - keeps access management separate from aws

<img src="img/aws11.PNG" style="width:100%">

* creating a user 

<img src="img/aws12.PNG" style="width:100%">

* a best practice is to create a group with certain permissions than add users to it

<img src="img/aws13.PNG" style="width:100%">

* add the user

<img src="img/aws14.PNG" style="width:100%">

* access keys are used to make programmatic calls to aws usnig cli

<img src="img/aws15.PNG" style="width:100%">

* generate an access key

<img src="img/aws16.PNG" style="width:100%">

# [`Creating an EC2 Instance`]

* in the console select the EC2 service

<img src="img/aws17.PNG" style="width:100%">

* configure the machine name ,os and specs

<img src="img/aws18.PNG" style="width:100%">

* u can ssh to the mashine using ssh key pair :
    - create a key pair
    - shh -i <file.pem location> ec2-user@<public IP@ of the machine>
* network settings set the vpc to default and the subnet for no-prefernce for a simple config

<img src="img/aws19.PNG" style="width:100%">

* set inbound rules to allow http ,https and ssh traffic

<img src="img/aws20.PNG" style="width:100%">

* add an IAM role to enable the instance to access other services 
* is this case an s3 & dynamodb full access custom role

<img src="img/aws21.PNG" style="width:100%">

* optional script to config configure the machine (or use ssh)

<img src="img/aws22.PNG" style="width:100%">

# [`EC2`]

* On AWS, compute options are:
    - EC2 (Virtual Machines): Emulates physical servers.
    - Containers (EKS): For lightweight, scalable apps.
    - Serverless (lambda): Runs code without managing servers.
* Amazon EC2 provides secure, flexible virtual servers (instances) in the cloud
* an AMI is a prebuilt EC2 oprimized image
* it's possible to create an AMI from an instance (usefull for creating instances)

<img src="img/aws23.PNG" style="width:100%">

* instance type & size :
    - size : storage size
    - type : usecases and the need (g:graphical intensive apps ,m5:general use)
    - memory optimized ,graphic optimized ,compute optimized ,..

<img src="img/aws24.PNG" style="width:100%">

* the EC2 instance can be modified and updated :
    - actions => instance settings => change instance type
    - you can change the instance type and rescale it's size

<img src="img/aws25.PNG" style="width:100%">

* EC2 instance life cycle :

<img src="img/aws26.PNG" style="width:100%">


# [`Serverless`] 

* serverless services allow users to focus on developping an app while letting aws take full care of the infrastructure

## `fargate` :

* lets you run containers without managing servers, you define the containers and Fargate handles the scaling and infrastructure

<img src="img/aws27.PNG" style="width:100%">

## `lambda` :

* service to run code in response to events (like file uploads or HTTP requests) without managing servers
    - autpmaticly scalable
    - highly available
    - all maintenance is tken care off
    - lambda functions are used for small services that dont require heavy load 
    - each lambada function work on its own environment
    - functions scale up or down based on the load

<img src="img/aws28.PNG" style="width:100%">

# [`VPC`]

## `subnets & gateways` :

<img src="img/aws30.PNG" style="width:100%">

* create a vpc 

<img src="img/aws31.PNG" style="width:100%">

* create a subnet 

<img src="img/aws32.PNG" style="width:100%">

* create a gatway to allow connection to the internet

<img src="img/aws33.PNG" style="width:100%">

* attach gateway to vpc

<img src="img/aws34.PNG" style="width:100%">

* a best practice is to duplicate resources hosted in an AZ to another one to ensure avilability
    - create similar subnets but in a different AZ 
    - duplicate and deploy resources in a different AZ

## `route tables` :

* when creating a vpc the default main route table allow traffic between all subnets

<img src="img/aws35.PNG" style="width:100%">

* create custom routetables for subnets based on the need (private|public)

<img src="img/aws36.PNG" style="width:100%">

* create a route table

<img src="img/aws37.PNG" style="width:100%">

* allow internet traffic to a public subnet

<img src="img/aws38.PNG" style="width:100%">

* attach the internet gateway

<img src="img/aws39.PNG" style="width:100%">

* attach the route table to the public subnets (subnet associations => edit subnet associations )

<img src="img/aws40.PNG" style="width:100%">

<img src="img/aws41.PNG" style="width:100%">

# [`NACLS & Security Groups`] 

## `nacls` :

* nacls are firewalls configured at the subnet level
* default nacls allow all in/out network traffic

<img src="img/aws42.PNG" style="width:100%">

* nacls are stateless ,both in & out rules must be configured for a specific protocol to fully allow it's traffic

<img src="img/aws43.PNG" style="width:100%">

<img src="img/aws44.PNG" style="width:100%">

## `security groups` :

* security groups are firewalls configured at the instance level
* the default security group config blocks all inbound and allows all out of bound traffic

<img src="img/aws45.PNG" style="width:100%">

<img src="img/aws46.PNG" style="width:100%">

* acls allows and denys traffic (evrything is allowed) unlike security groups wich only allow traffic (evrything is blocked)

