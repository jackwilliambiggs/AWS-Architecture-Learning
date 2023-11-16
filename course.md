
# AWS Architecture Course

skamal@amazon.co.uk  is the contact number 

6 years with AWS - joined as a devops engineer moved towards AWS 

Important to ask questions. 

Lunch break is 1200 to 1300. 

Link to the book that we will be learning from https://online.vitalsource.com/reader/books/200-ARCHIT-76-EN-LG-E/pageid/0

The lab is only available for the next 30 days 

However the books are available to us for the next two years. 

In addition to the lab book there is the supplement book too: https://explore.skillbuilder.aws/learn/course/external/view/elearning/8319/architecting-on-aws-online-course-supplement

It allows you to go go through each topic at depth for the course. 

## Architecting Fundamentals 

Amazon Web Services: Anything that you want to odo there is a service to get to that component.

10000 plus services. 
More than 200 services

Lots more agility and less complexity and risk 

Agility: better time to market (TTM), Increase innovation, scale seamlessly 
Complexity and risk: Optmize costs, Minimise security vulnerabilities and reduce management complexity. 

Instead of quarters and months you start talking more in terms of days and weeks. 

### Service Categories 

We'll focus on:
Severless, Networking, Database, Security, Management and Governance, Storage, aws cost management, Compute and Containers.


## Cloud Cost Components
- Compute 
- Storage 
- Data Transfer 
- licencing 
- Any other cost

### 3 ways to interact with AWS 

- Console (GUI) - User id + password
- AWS CLI - Access Key ID + secret access key
- AWS SDKs (Programmatic access) - Access Key ID + secret access key

there are very circumstances where the above can't do the same task. 

### AWS Global Infastructure

- Regions 
- Availability Zones 
- Edge Locations

An availability zone is made up of one or more Data Centers. 
A region is made up of multiple AZs

AWS Local Zones are used for things that require very low latency. The very first local zone was actually for hollywood.   

#### Edge Locations

CDN (content delivery network): copy (caching) content and then move it to the nearest edge location. They therefore make sure that they get the best possible latency.

The service to do this is cloudfront AWS. The Edge case locations are the special purpose built locations where they are mvoeing the data 

Unlike AZs Edge zones are seperate to availability zones. 

There are currently 600+ Points of Presence (PoPs). 

#### Amazon Backbone Network

Amazon have cables all across the world to connect all of there regions. So in theory each datacentre will have a physical connection to every other data centre that AWS offers. 

Some of the cables are even underseas: you can see some of the cables with: https://www.submarinecablemap.com/. 


### AWS Well-Architected Framework 

Good to google AWS well architected framework 
Go to the whitepaper for one of the six pillars and then look at the design principles. 
These papers are good the why and what. 
How you implement the well architected aspects: https://www.wellarchitectedlabs.com/ 


## Account Security 

### Access Management on AWS

- IAM (Identity and Access Management)
   - Users
   - Groups 
   - Policies
   - Roles


** 3 A's of security**

Authentication: You are who you say you are 
   - What you know --> Credentials 
   - What you have --> Soft ws well as Hard Tokens, OTP
   - What you are --> Biometrics
Authorisation: Once you are in the system what you can do.
Account: Auditing: Who has done what, Investigation purposes.


Authentication for AWS
   - Users 
Authorisation
   - Policies
    - Identity bases 
        - AWS Managed Policies 
        - Customer Managed Policies
    - Resource based
   - Groups
   - Roles 
Accounting
   - CloudTrail


Root user: each time you create an AWS account you will need to create Root 

You should not use your root account for the day to day activities

### IAM 

Users: We all have our own user accounts

RBAC role based access control 
Least required access 

Best Practice: Anything that you don't need you should not have. 

1) Assign permissions to groups 
2) Put users in groups 

### Roles

- Temporary access to elevated prividlegd
- Federated Access: 
- Application to service/resource access

Temporary access: 

Temporarly elevated priviledges 

Redhat: yum install httpd --> sudo yum install httpd 
Microsoft: Run as admin

Federated access:

Say you want to access another environment but don't want to create another user on that environment
You create 'role' that users from another environment can attach to. 

How it works 

Session tokens
minumum duration is 15 minutes and the maximum duration is 36 hours.


### Security Policies 

Identity based policy

With policies you can set a multitude of conditional factors to enable access 
for instance you can allow certain actions based on a specific date range or a a specific region. 

Always have to explicity allow users are set up with the implicit deny. This intuitively should make sense 


### Multi accounts 

Any decent organisation will have multiple accounts. They can create multiple accounts whilst maintaining a single organisational account. This assists with billing.

Service Control Policies: control the behaviour/access at the account level. 


### Networking in AWS [Part-1]

- VPC 
   **Routing**
   - Subnets
   - Route tables 
   - Internet Gateway 
   - NAT Gateway 
   - Elastic IPs 
   - ENIs 
   **Security**
   - Security Groups 
   - Network ACLS 


172.31.0.0/16

What is the significance of the 16? 

This is telling us how many bits are dyanmic. Essentially we are blocking the first two octet for instance 172 is fixed, 31 is fixed, third 0 can move and the fourth octet can move

So: 172.31.{0-255}.{0-255}

Here are some more examples of CIDR notation

10.0.0.0/8 -> 10.{0-225}.{0-225}.{0-225}
192.168.0.0/24 -> 192.168.0.{0-255}
0.0.0.0/0 <- represents all of the IPs in the world
1.2.3.4/32 -> 1.2.3.4 in CIDR format Single host

There are 32 bits in an Ipv4 IP address - there are four octets. 
Ipv6 has 128 bits. 

There is a paper that is the reason why we are able to still use IPv4: https://www.ietf.org/rfc/rfc1918.txt 

The default VPC CIDR range is 172.31.0.0/16 

### VPC Funamentals 

Logical boundary: create a CIDR range. 

Subnets can be private or public. 

VPC is one big range, you then divide them into subnets which are just dividions of the range.

Public <- Can reached from the outside world
Private <- Cannot be access from the outside world.

You need an internet gateway to connect to an

Route tables are used to control where network traffic is directed.

NAT gateway enables the private subnet to connect to the internet. Important to add that only eggress is permitted here not ingress. 

### VPC Traffic Security 

Filtering traffic 

- Security group are firewall at the instance level
 
 Default behaviour is that it blocks all inbound traffic and enbales all outbound traffic. 

- 
## Compute on AWS

- Virtual Machines
  - EC2 instance
- Containers 
  - ECS
  - EKS
- Severless 
  - Lambda (Function-as-a-Service)
  - Fargate (Severless Containers)

When you create an EC2 you are basically creating a virtual machine inside a big AWS computer

You can tag EC2 instances with metadata to help identify them. 

For isntance you would like to update the web servers in project x from apache version x to y. 

### EC2 Pricing Options 

- On-demand 
- Spot
   - Unused capactiy in AWS DCs 
   - upto 90% discount over on-demand 
   - Can be reclaimed back by AWS (2 minutes)
   - Excellent for any type of stateless workloads (the data from the code, or from compute is seperate). Session data is seperate.
- Commitment based 
   - Reserved Instances
   - Savings Plans 
- Hardware isolation 
   - Deicated Instances
   - Dedicated hosts

Irrespsective of price the hardware should perfom the same


### Amazon Machine Image

when you create an EC2 instance you need to understand the template that you would like for your workload.

Naming conventions: 

c6g.xlarge
c <- instance family
6 <- instance generation
g <- additional properietes
xlarge <- the size of the instance 

For a full list of the types of EC2 instance that there are look here: https://aws.amazon.com/ec2/instance-types/

instance generation - rule of thumb is that you should always go for the latest generation.

later generations tend to provide the best price to performance ratio. 

User Data: enable you to pass on script to be run on the instance. 

### Storage for EC2 instances 

Started day 2 here. 

Object 
   - S3  

Block 
   - EBS | Persistant Block Storage
      - SSD Based
      - HDD Based 
   - Instance Store | Ephemeral Block instance
File/Network | NAS - Network attached storage
   - EFS | Linux Workloads | Network File System 4.0 and 4.1 
   - FSx | Windows workloads | CIFS, NTFS, SMB. 


EBS Volumes 

SSD and IOPS SSD 

What you should focus on is the use cases for the two different General Purpose SSD and IOPS SSD Volumes. 

Instance Storage

Once you have stopped the EC2 instance all of the data is lost. 

Try and understand SAN implementation and a DAS  (Direct Attached storage) implemetnation. 

**research different file systems**

### AWS Lambda 

Severless computing <- Servers are fully managed by AWS.

You focus on the codebase - any scaling, troubleshooting are focused on by AWS.

90s EC2 instances
2000s ECS and EKS 
2010s Lambda and Fargate 


Serverless has the unique ability to scale to zero. 

This is really good when you have hardly any customers. 

Lambda is something that is triggered as response to an event. 

Functions can only run for 15 minutes (when you are writing a function you have to make sure that the function takes no longer for 15 minutes). 

Web applications
Backends 
Data Processing 
Data Procesing 
chatbot
amazon alexa 
IT Automation. 

If you can divide you application or function into multiple 

It is event driven architecture i.e one of the AWS services  
S3 Trigger i.e an image processing application 

### Storage



block storage C:/ d:/  DAS or SAN 

file storage G: K: <- Network storage NAS 

So block storage is local. Hard disk. 

Instance store directly attached to the motherboard 

NAS think of lan cables. You now have 100gb speed in LAN cables. 

#### S3 

Folder/directory in the cloud that gives you unlimited Object Storage.

The way that Amazon works to ensure that there are 99.999999999% durability is through replication. 
This replication is achieved with SRR (Same Region Replication) and CRR (Cross Region Replication)

Access Control 
   - block public access
   - Bucket ACLs
   - bucket policy (reccomended)
   - CORS 

Storage Classes 

These are based on the frequency of the data being access. 

S3 Standard - something that is being accessed frequency 
Glacier the other end of the spectrum. 
S3 Glacier is the least frequency. 

Very important to choose the right storage class as impacts cost significantly. 

Glacier is far cheaper than S3.

S3 intelligent tiering 

AL/ML intelligent enough to make a decision on your behalf. 


S3: Pay for what you use. 
EBS: Pay for what you provision.
File network: pay for what you use.


Thin or Thick Provisioning: 

#### Data migration tools 

Online migration: you move data over the internet there are a few thigns AWS stroage Gateway, AWS DataSync, AWS Transfer family 
Offline migration: AWS Snow Family.


##### Storage Gateway 

There are multiple gateways based on the storage protocol for instance you'd use the relevant storage gateway product for SMB. 


### Databases

Huge portfolio of services. 

- Relational
   - RDS
      - Maria 
      - Postgre
      - MSSQL 
      - MySQL 
      - Aurora 
      - Oracle 
   - RDS Features 
      - Multi-AZ
         -  High Availability. 
      - Read replicasd
         - Performance optimisation 
 - Non-relational 
   - DynamoDB 
Database Caching
   - Elasticache 
      - Redis
      - Memcahced
- Other purpose-built databases
    - Data Warehousing 
       - Redshift 
   - Graph DB 
       - Neptune 
   - BlockChain 
      - WLDB 
   - Timeseires 
      - Time Stream 


    

When you select for Multi-AZ deployment you end up with a standby DB instance, in the event of a failure a secondary or standby database will be created in another database zone.  

there also read replicas - with this you can send all of the read requests to the replica database. 
You can even have read replicas in other regions. 


Lazy Loading
First try the cache 
Then see that cache doesn't have everything that you need
Missing data that the application request from the database is taken
data is then return to the application 
The final step is that the cache is updated with the missing data

The benefits of lazy loaded is that only the data that is being accessed are being placed in the cache. 


Write-through

Whenver you do an update to database - application will also write the data to the cache 
The benefits are that there will not be any cache miss but you are copying over information that you might not use again 

cache node = servers. 


Amazon Elasticache 


Important to look at the difference of ElasticCache for maemcached and for redis


MySQL (on-prem) ---? AWS DMS ---> MySQL (on Amazon RDS)
MySQL (on-prem) ---? AWS DMS + SCT  ---> Aurora (on Amazon RDS)

If you are chaning the type of database you'll need the schema change service. 



#### Auto scaling


- Launch Templates (What needs to be created)
- Auto scaling Groups (how many instances need to be configured at any time) i.e you set a 
- Auto Scaling group 
   - Scheduled: Predicable workloads 
   - Dynamic: General scaling
   - Predictive: Intelligent it works on ai/ml trained models (uses your applications historic data and creates a forecast). 


Group capacity you can set the scale for minumum normal and  maximum EC2 instances

Ansible vs Terraform 
Cloudformation for SSM


### Automation on AWS

- Infrastructure as Code
   - Cloud Formation 
   - CDK (Cloud Development Kit)
   - Terraform 
   - EC2 Image Builder
   - Packer

Configuration Management (Maintain the state of the tools)
   - AWS Systems Manager
   - AWS Config
   - Puppet 
   - Chef 
   - Ansible 

Amazon codewhisperer is something that seems akin to Amazon CodeWhisperer. 

### Containers 

Container eco-system

#### Container runtimes 

The software that you need to run containers. 

The most popular is docker 

But there are also 

- rkt 
- cri-o 
- containerd 
- podman 
- Singularity 

This is a piece of software that gives you the ability to create containers. 

You can work with tens of thousands of containers. You will typically run with thousands of containers. 
It is not possible to work with containers on an individual basis. 

For this reason you need a form of a container orchestration engine 

#### Container Orchestration Enginges (COEs)

- Kubernetes (this is actually the biggest software on the planet at the moment). 

| Component | Description |
| --- | --- |
| **CRI (Container Runtime Interface)** | The Container Runtime Interface is a critical component in Kubernetes that defines the interface between Kubernetes and the container runtime. It enables pluggability, allowing different container runtimes (e.g., Docker, containerd, cri-o) to be used with Kubernetes. |
| **CSI (Container Storage Interface)** | The Container Storage Interface is a specification that standardizes how container orchestration systems, like Kubernetes, interact with storage systems. It allows storage providers to develop a single CSI driver for use across various container orchestration platforms. |
| **CNI (Container Network Interface)** | The Container Network Interface is a specification and standard for defining how container runtimes should set up networking for containers. In Kubernetes, CNI is responsible for configuring network interfaces in pods, allowing communication with each other and the external network. |


#### Mircoservices

Microservices is when you split workload i.e EC2 instances, storages 

Benefits:- 

- Code can be updated in isolation. 
- Decouple.
- Highly reusable. 
- Individual SDLC.
- You can also write in multiple languages - so multiple microservices essentially. 

A monolithic architecture means that if one aspect of everything fails the whole service will fail. 



#### Containers vs VM 

- Virtual Machines --> Hardware level virtualisation. 
- Containers --> OS/Kernel level Virtualisation.  (Shares the OS with the host). Containers are nothing more than a process to the host machine basically. 

containers are like ultra light weight virtual machines <- good statement but technically a completely differnt type of virtualisation. 

Each container is comprised:
- Code 
- Configuratoin 
- Dependencies 
- Run time engine. 

When you package everything you have just what you need and nothing else. 

This is what makes this self contained and repeatable and portable. 

In a monolithic world everything revolved around: Inter process communication. 


#### Containers on AWS

- ECR | This is where you save your images (blueprint of the desired containers).

- ECS | Amazon's Proprietry software 
   - Started in roughly 2014. Provided the control chain, where you have some worker nodes. 
- EKS | Hosted Kubernetes on AWS

- Fargate 
   - Fully managed 

- Amazon EC2 
   - Partially managed 

 
































  





















### Keywords 





