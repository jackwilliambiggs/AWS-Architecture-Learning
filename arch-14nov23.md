

Exam Prep: Solutions Architect - Professional --> https://explore.skillbuilder.aws/learn/course/external/view/elearning/14951/exam-prep-standard-course-aws-certified-solutions-architect-professional-sap-c02


### Keywords
- Undersea cables / Submarine cables
- SDDC (Softwared Defined Data Centres)
    - Server Virtualization (ESXi/HyperV/KVM)
    - Storage Virtualization (SAN)
    - Network Virtualization (SDN/NSX)
- DAS vs SAN vs NAS
- Monolithic --> Service-Oriented-Architecture --> Microservices
- Shared Tenancy Model
- Thin vs Thick Provisioning
- False positives
- Kubernetes
    - OCI
    - CRI
    - CSI
    - CNI

### Cloud Cost Components
- Compute 
- Storage
- Data Transfer
- Licensing
    - Pay as you go
    - BYOL
- Any other cost


### 3 ways to interact with AWS:
- Console (GUI) - User id + Password
- AWS CLI (Command Line) - Access Key id + secret access key
- AWS SDKs (Programmatic access) - Access Key id + secret access key
- CloudShell - Available on AWS Console

### AWS services can have:
- Soft limits/Quotas 
    - 100 buckets per account (S3)
    - 1000 invocations (Lambda)
- Hard limits/Quotas
    - 15 Minutes of execution time (Lambda)
    - 5TB Max object size
**View "Service Quotas" to check your account specific limits**

### AWS Services can be:
- Managed   --> S3, ELB
- Unmanaged --> EC2

### AWS Service Scope can be:
- Global        --> IAM, Route 53
- Regional      --> VPC, DynamoDB
- AZ Specific   --> EC2, EBS, Subnets


### AWS Global Infrastructure
- Regions | 32 Regions
- Availability Zones (AZs) - 102 AZs
- Edge Locations | CDN | Web content caching | 600+ PoPs
- Local Zones | 55+
- Amazon Backbone Network


### Access Management on AWS
- IAM (Identity and Acess Management)
    - Users
    - Groups
    - Policies
        - Identity based
            - AWS Managed
            - Customer Managed
        - Resource based
    - Roles
        - Temporary elevated privileges
        - Federated access
        - Application to service/resource access

**3 A's of security**
A - Authentication (2FA / MFA)
    - What you know --> Credentials 
    - What you have --> Soft and hard tokens, OTP
    - What you are  --> Biometrics
A - Authorization
A - Accounting (Auditing / Investigation)

**3 A's in AWS**
- Authentication
    - Users
- Authorization
    - Policies
    - Groups
    - Roles
- Accounting
    - CloudTrail

#### Multi-account Architecture
- AWS Organizations
    - SCPs (Service Control Policies)


### Networking in AWS [Part-1]
- VPC
  **Routing**
    - Subnets (Similar to VLANs)
        - Private subnets
        - Public subnets
    - Route tables
    - Internet Gateway
    - NAT Gateway
    - Elastic IPs --> Static IPs on AWS (BYOIP)
    - ENIs --> NIC (Network Interface Card) --> vNIC ---> ENI (Elastic Network Interface)
  **Security**
    - Security Groups
        - Firewall at the instance level
        - Default: All incoming blocked, all outgoing allowed
        - No deny rules; only allow
        - No rules precedence
    - Network ACLs
        - Firewall at the subnet level
        - Default: all incoming/outgoing allowed
        - Both allow/deny rules are supported
        - Rules precedence supported

**CIDR Notation**
10.0.0.0/8      --> 10.{0-255}.{0-255}.{0-255} --> 256x256x256 --> 16,777,216
172.31.0.0/16   --> 172.31.{0-255}.{0-255} ---> 256x256 --> 65,536
192.168.0.0/24  --> 192.168.0.{0-255} --> 256
0.0.0.0/0       --> All IPs in the world / Internet
1.2.3.4/32      --> 1.2.3.4 in CIDR format


### Compute on AWS
- Virtual Machines
    - EC2
- Containers
    - ECS
    - EKS
- Serverless
    - Lambda (Function-as-a-Service)
    - Fargate (Serverless Containers)


#### EC2 Pricing Options
- On-demand
- Spot
    - Unused capacity in AWS DCs
    - upto 90% discount over on-demand
    - Can be reclaimed back by AWS (2 minutes)
    - excellent for stateless workloads
- Commitment based
    - Reserved Instances
    - Savings Plans
- Hardware isolation
    - Dedicated Instances
    - Dedicated Hosts


### AWS Storage Portfolio
- Object
    - S3 | Internet accessible Unlimited Object storage | Pay for what you use
        - 99.999999999% durability
        - Replication
            - SRR
            - CRR
        - Access Control
            - Block Public access
            - Bucket ACLs
            - Bucket Policy (recommended)
            - CORS
        - Storage Classes
        - Lifecycle policies
        - Intelligent tiering
        - Versioning
        - transfer acceleration
        - Multiplart upload

- Block
    - EBS | Persistent Block Storage | SAN | Pay for what you Provision
        - SSD Based
        - HDD Based
    - Instance Store | Ephemeral Block Storage | DAS

- File/Network | NAS | Pay for what you use
    - EFS | Linux workloads | NFS 4.0 and 4.1
    - FSx | Windows workloads | CIFS, NTFS, SMB



### Databases on AWS
- Relational
    - RDS Engines
        - Maria
        - Postgre
        - MSSQL
        - MySQL
        - Aurora
        - Oracle
    - RDS Features
        - Multi-AZ
            - High Availability
            - Synchronous replication
        - Read Replicas
            - Performance optimization
            - Asynchronous replication
- Non-relational
    - DynamoDB
- Database Caching
    - ElastiCache
        - Redis
        - Memcached
- Other purpose-built databases
    - Data Warehousing
        - Redshift
    - Graph DB
        - Neptune
    - BlockChain
        - QLDB
    - Timeseries
        - Timestream

Ref: https://aws.amazon.com/products/databases/

**Database Migration** 
MySQL (On-prem)  ---> AWS DMS ---> MySQL (on Amazon RDS)
MySQL (On-prem)  ---> AWS DMS + SCT ---> Aurora (on Amazon RDS)

DMS Workshop: https://catalog.us-east-1.prod.workshops.aws/workshops/464d6c17-9faa-4fef-ac9f-dd49610174d3/en-US/migration/dms


### Monitoring on AWS
- CloudWatch
    - Metrics
        - Basic monitoring
            - Enabled by default
            - Free tier eligible
            - 5 minutes granularity
        - Detailed monitoring
            - Has to be enabled
            - Extra pricing applicable
            - 1-minute (or less) granularity
    - Logs
    - Alarms and Events
    - Dashboards

Ref: 
1. https://catalog.us-east-1.prod.workshops.aws/workshops/31676d37-bbe9-4992-9cd1-ceae13c5116c/en-US
2. https://aws.amazon.com/cloudops/monitoring-and-observability/

### Load balancing on AWS
- ELB (Elastic Load Balancer)
    - ALB | Layer 7 | http and https | Content/path based routing
    - NLB | Layer 4 | tcp, udp, ssl, tls | IP based routing
    - GLB | Layer 3 | Ip filtering | hosted security appliances

**Content/path based routing**
amazon.co.uk/home
            /wishlist
            /orders
            /productA
            /productB


### Auto scaling
- Launch templates (What needs to be created)
- Auto Scaling Groups (How many)
- Auto Scaling Policy (When)
    - Scheduled
    - Dynamic
    - Predictive


### Automation on AWS

- Infrastructure-as-Code (Provisioning the resources)
    - CloudFormation
    - EC2 Image Builder
    - CDK (Cloud Development Kit)
    - Terraform
    - Packer

- Configuration Management (Maintain the state)
    - AWS Systems Manager
    - AWS Config
    - Puppet
    - Chef
    - Ansible

Ref:
1. https://cdkworkshop.com/


### Containers on AWS

#### Container Runtimes
- Docker
- rkt
- cri-o
- containerd
- podman
- Singularity

#### Container Orchestration Engines (COEs)
- Kubernetes
- Docker Swarm
- Open shift
- Mesosphere
- ECS
- EKS

#### Microservices benefits
- Code can be updated in isolation
- Decoupled
- Reusability
- Scalability
- Individual SDLC
- Different languages can be used for different microservices

#### Containers vs VM
- Virtual Machines --> Hardware level Virtualization
- Containers    --> OS/Kernel level Virtualization

#### AWS Container Services
- ECR | image Registry
- ECS | Amazon's proprietory software 
    - EC2 Mode 
    - Fargate Mode 
- EKS | Hosted Kubernetes on AWS
    - EC2 Mode 
    - Fargate Mode 


### Networking on AWS [Part-2]
- Connectivity/Hybrid
    - VPC Peering
    - Trasit Gateway
    - VPN
    - Direct Connect
    - VPC Endpoints
        - Gateway Endpoints
            - S3 and DynamoDB
            - Requires route table mofifications
        - Interface Endpoints
            - Almost all the other services
            - Does not require route table modifications


### Serverless on AWS
- What is EDA? (Event Driven Architecture)
- API gateway (API SDLC management)
- SQS (Poll based Message Queue)
- SNS (Notifications)

Ref:
Error handling in Serverless: https://aws.amazon.com/tutorials/handle-serverless-application-errors-step-functions-lambda/



### References
- https://aws.amazon.com/about-aws/global-infrastructure/
- https://www.submarinecablemap.com/
- https://aws.amazon.com/architecture/well-architected/
- https://www.wellarchitectedlabs.com/
- https://aws.amazon.com/developer/tools/
- https://aws.amazon.com/cli/
- https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_examples.html
- https://docs.aws.amazon.com/pdfs/whitepapers/latest/tagging-best-practices/tagging-best-practices.pdf
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html
- https://ec2spotworkshops.com/
- https://aws.amazon.com/products/databases/
- https://d0.awsstatic.com/whitepapers/performance-at-scale-with-amazon-elasticache.pdf
- https://catalog.us-east-1.prod.workshops.aws/workshops/464d6c17-9faa-4fef-ac9f-dd49610174d3/en-US/migration/dms
- https://docs.aws.amazon.com/pdfs/whitepapers/latest/introduction-devops-aws/introduction-devops-aws.pdf
- https://owasp.org/www-project-top-ten/
- https://docs.aws.amazon.com/pdfs/whitepapers/latest/aws-best-practices-ddos-resiliency/aws-best-practices-ddos-resiliency.pdf
- https://aws.amazon.com/blogs/architecture/disaster-recovery-dr-architecture-on-aws-part-i-strategies-for-recovery-in-the-cloud/





