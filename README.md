# Azure Tutorial

## Azure Compute Services

Ways to reduce Cost of Virtual Machine

- Reservation - You can reserve your instance between 1-3 years which can can get you upto 56% cost reduction. This is good for Production that runs continuously.

- Spot on - These are instances that is not used by azure which you can use at a cheaper rate but your server can be shutdown at a short notice

- Disk Optimization - This is determined by the type of disk you are using example
  1. Default is the premimum SSD - This is the most expensive option
  2. Non - IO intensive machines can do with Standard SSD
  3. Not the disk type can affect the SLA

## Techniques to reduce Cost

1. Select the right size for your machine
2. Select linux over windows when possible
3. Check the price in the nearby regions

## Availability of VM

- Fault Domain - Logical group of physical hardware that share a common power source and network swich. A rack is also know as a fault domain and if let say the power of a rack goes down all the servers on that rack goes down.

- Update Domain - Logical groupd of physical servers that goes to maintenance and be rebooted at the same time. servers in update domain can be spread across fault domain

- Availability Set - A collection of fault domain and update domain your VM will be spread across. It can contain upto 3 fault domain and 20 update domain. All the fault and update domain is in the same data center. Availability set is suitated in the same zone(building)

## Availabiliity Zone

- A physically seperaate zone within an Azure region

## Azure Resource Manager Template

This is a JSON file that describe the resources Azure wants to create. It is used by azure in almost all the resources. It can be modified, created and deployed. It uses declarative to create resources

Difference between Declarative and Imperative

Declarative

- It describes the end results
- It can deploy multiple resources at once
- Can be integrated into CICD processes
- Can be source controlled
- Used by ARM Template
- Best used to create an environment

Imperative

- Sends instructions to run
- Error prone
- Can't be verified
- Can't be source controlled
- Suited for quick and dirty operations
- used by Azure CLI, Powershell
- Best used to create virutal machine

## Virtual Machine Scale Set

- A group of seperate VM sharing the same image
- Managed as Group
- Can be scaled out or in manually or according to predefined conditions.
- Great for handling unpredicated load.
- once set up should not be modified - example installing application or changing files. This will be removed when it scales out.
- New machine created by scale set will be based on original image
- For web application load balancer should be added to the front.

## Azure Instance Metadata Services (video 14)

- A little known feature of Azure VMS
- A REST API accessible from the VM
- Providing a lot of info about the machine
- Info includes:
  - SKU, storage, networking, scheduled events
- Accessibile ONLY from the VM
- With Scaleset
  - Get Notification about upcoming eviction
- Can be polled every ~1 min to get enough time to close things up

`Practical videos starts at video 15 in azure compute folder`

## App Services

- A fully managed web hosting for websites
- Publish your code and it just runs
- No access to the underlying servers
- Secured and compliant
- Integrates with many source controls and DevOps Engines
  - Github, BitBucket, Azure Devops, DockerHub and More
- Supports Platforms
  .NET, .NET Core, Nodejs, Java, Python, PHP
- Support Containers
- Support the following App Types:
  - Web Apps
  - Web Api
  - Web Jobs(Batch Processes)

### How to Deploy to App Service

- Develop the app
- Create Web App
- Publish the Code
- Viola

### App Services Tiers

- Standard Tiers - Offers the Right combination of performance and scale for most web apps
- Free - Offers a limited storage space and computing power. It uses shared server
- Isolated - It offers a completely isolated plan. it sits on it own private network

## Azure Kubernetes Services (36)

- Managed Kubernetes on Azure
- Allows deploying containers and managing them using kubernetes on Azure
- Paying only for the instances used

## Azure Functions (38)

- Small focused functions running as a result of an event
- Great for Event Driven Systems
- Automatically managed by Azure
  - Start, stop, autoscale
- Flexible pricing plans
- Serverless

## Servless (38)

- Cloud resource that is completely managed by the cloud
- Users do not need to think about
  - VMs, CPU, Memory etc
- It just works

### Triggers

- These are events that makes the functions run
- Quite a few
- It is not mandatory
- example
  - Rabbit MQ, Queue Storage, Service Bus, Timer, Kafka, IOT Hub, etc

### Binding

- Declarative connection to other resource(s)
- Input, output, or both
- Provided as a parameter to the function
- makes connecting to other resources extremely easy
- Not mandatory
- example
  - Rabbit MQ, Queue Storage, Service Bus, Timer, Kafka, IOT Hub, etc

### Cold Start

- Azure functions are completely managed by Azure
- After sometime of inactivity Azure might take down the functions host
- The next activation of the function will take time
  - It can take 2-3 seconds befor the code runs
- A problem mainly for http-triggers

### Soluton

- Select the right Hosting plans

### Azure function Hosting Plan

- Consumption
- Premium
- Dedicated

### Consumption

- You pay for what you use
- Limit of 1.5 GB RAM

### Calculation

- Executions/month: 9m
- Avg. memory consumed/execution: 800mb
- Avg. execution duration: 1.5s
- Total Seconds: 9m \* 1.5s = 13.5m secs
- Total GB/Sec = 13.5m \* 0.8 = 10.8m - 400K free grant = 10.4m GB/sec
- Payment for execution time: 10.4m \* 0.000016$ = 1.66.4$
- Payment for executions: 9m-1m free grant = 8m \* 0.3$/m = 1.6$
- Total Payment: 168$

### Downside

- Cold Start
- Limit of 1.5GB
- Unpredictable Pricing

## Premium Plan

- No Memory limit
- No Cold Start
- Better Performance
- VNet Integration
- Predictable Prices
- More Expensive

### Calculation

- 1 pre-warmed instance
- 2 vCpus, 7GB RAM
- No scale out
- vCPU cost: 123.37 \* 2 = 246.74$
- Memory cost: 8.833&7 = 61.83$
- Total Payment: 308.57$

## Dedicated Plan

- The functions run on an existing App Service
- Great if server is under-utilized
- No additional costs
- Make sure Always On setting is activated to avoid disabling the function

### Downsides

- No Auto-scale support

## Durable Functions

- Stateful Functions that interact with external resources and keept track of flow
- Offer very simple syntax, hide complexities of managing state, retries, etc
- example - Function chaining - Call various functions squentially, and apply the output of each function to the next one

## How to choose the Right Compute Type (34)

## More Compute Options

- Logic Apps - it integrate with other azure services to execute logics
- ACI - Azure Contaienr Instance - it runs docker container without AKS. You can run a single container on it
- App Service Container - You can deploy docker to App Service

## Azure Networking

- Networking is the basics for cloud security

## 2 Main Threats of exposing your VM or port number to the public

- Brute force attack on the port
- No line of defence in front of the VM

## Azure Networking Services

There are 4 Azure networking services

- VNet
- Subnets
- LoadBalancer
- Application Gateway

### Virtual Networks (VNets)

- A network which you can deploy cloud services example, VMs, App Service, DB etc
- "Virtual" as in "based on Physical Network" and logically seperated from other Virtual Networks"
- Resources in VNet can communicate with each other by default.
- VNets are free
- Limit of 50 VNets per subscription
- Scoped to a single region - cannot span across region
- Scoped to a single subscription
- can be connected by Peering
- segmented by subnets
- Protected by NSGs (on the subnets)
- Each VNet has a range of address range called IP range. By default 65,536 address

### CIDR Notation

- Classless inter-domain routing
- A method for representing an IP range
- Composed of an IP address in the range and a number between 0 and 32
- It indicates the number of bits that is allocated to address. The smaller the number the larger the range.

### Subnet

- Logical segment in the VNet,
- Shares a subnet of the VNet IP range
- Used as a logical group of resources in the VNet
- Resources must be placed in a subnet cannot be placed directly in the VNet
- Resources in different subnet and the same VNet can communicat with each other

### Addresses of Subnet

- Each subnet gets a share of the parent VNet IP range
- Never use the full range of the VNet in a subnet
- subnets are free
- limits of 3000 subnets

` Pratical videos starts at 006`

### Network Security Group

- A gate keeper for subnets
- Defines who can connect in and out of subnets
- look at it as a mini firewall
- it is free

### How NSG Work?

- Looks at 5 tuples
  - Source (Where did the connection come from)
  - Source Port (The port the source is using)
  - Destination (Where does the connection request goes)
  - Destination (To which port does it want to connect)
  - Protocol (TCP, UDP, Both)
- This is called Security Rule
- NSG is automatically created and attached to every newly created VM's network interface
- NSG by default opens RDP on windows and SSH on linux to anyone
- Must be handled after creation.

### Network Peering

- Sometimes you need to place some resources in seperate VNet to enhance security. Eg. Seperate system, System layer(FE, BE), Database
- Reason so we don't place resources that does not require public acces to be placed in VNet that has public accesss
- Network Peering is when we allow one VNet to interact with each other
- make sure address spaces are not overlapped otherwise we can not peer the VMs
- use NSG for protection
- Peering can work accress region
- Network peering is not free

` Pratical videos starts at 15`

### Network Watcher

- This is used monitor the VNets and subnets

### Secure VM Access

- Leaving public IP open is always a risk we want to avoid
- The larger the attack surface - the greater the risk
- We want to minimize it as much as possible.
- Not related to the design but important

### How to secure VM

- JIT Access
- VPN
- Jump Box
- Bastion

### Just In Time Access(JIT)

- Opens the port for access on demand, and automatically closes it.
- Closed the rest of the time
- Can be configured from VM page in the portal
- Required Security Center Liscense Upgrade

` Pratical videos starts at 19@40mins`

### Virtual Private Network

- A secure tunnel to the VNet
- Can be configures so that no one can connect to the VNet.
- Requires VPN software and liscense (not part of Azure)

### Jump Box

- Place another VM in the VNet
- Allow access ONLY to this VNet
- When need access to one of the VMs - connect to one and from there connect to others
- Only one port is open

### Bastion Host

- Web based connection to VM
- No open port is required
- Simple and Secure
- Cost - 140$/month

` Pratical videos starts at 20`

### Bastion Downside

- it requires portal access
- Cost

### Service Endppoint

- Alot of managed services exposes public IP. i.e, Azure SQL Server, App Service e.t.c
- Sometimes these resources are accessed from only resources in the cloud. e.g, database
- The pose a security risk
- Service Endpoint solves these security risk
- Creates a route from the VNet to the resources
- Traffic never leaves Azure backbone
  - Although the resource still has a public IP
- Enable Service Endpoint on the subnet from which you want to access
- On the resource, set the subnet as the source of traffic

### Private Link

- It extends managed service into the VNet
- Traffic never leaves the VNet
- Access to the internet is blocked
- It is not free
- VM talks to the App Service via private IP

### Difference between Service Endpoint and Private link

- Service Endpoint is a legacy solution (It is an old solution) while Private link is a newer version of service endpoint.
- Private Link support more resources than Service Endpoint.
- Service Endpoint is free while Private Link is not free
- Service Endpoint is simpler than Private Link
- On-Prem Connectivity of service endpoint is complex than Private Link

### App Service VNet Integration

- Allows access from app service to resources within VNet so that the resources should not be exposed to the public
- Extremely useful when App Service needs access to a VM with internal resources
- Supports same-region VNets. For VNets in other region a gateway is required

### Difference between Service Endpoint/Private Link and VNet Integration

- SE/PL allow traffic from a resource(eg Vm) to a managed resource such as app service while VNet Integration allows traffic from managed resource(App Service) to VNet.

`Practical video start at 24@02mins`

### App Service Access

- Similar to NSG - but for App service
- Restricts traffic to App Service
- By default - all inbound traffic is allowed (in relevant ports)
- We can restrict the inbound traffic to allowed IPs/VNets/Service Tag
- Main use cases
  - Backend App Service that should be accessed from frontend/VM only
  - Frontend App Service that should be accessed from load balancer only.
  - Open App Service to customer only to access it.

### App Service Environment

- App Service Environment
- Special type of app service deployed directly to a dedicated VNet
- VNet can be configured like any other VNet - Subnets, NSGs etc
- Created on dedicated Hardware
- Very Expensive
- Major Use Cases
  - Elevated security
  - Very high scale environement

### Load Balancer

- It distributes the loads and checks health of VMs
- When VM is not healthy - No traffic is directed to it.
- Can work with VMs or scale set
- can be public or private
- Operates at layer 4 of OSI model

### Load Balancer Distribution Algorithm

- Based on 5 tuple has:
  - Source IP
  - Source port
  - Destination IP
  - Destination Port
  - Protocol type

### 2 Types of Load Balancer

- Basic
  - No Redundancy - when a load balancer is down we are left with none
  - Open by default
  - support up to 300 instances
  - No SLA
  - Free
- Standard
  - Redundant - when a load balancer is down no one spins up automatically
  - Secured by default
  - support up to 1000 instances
  - 99.9% SLA
  - No Free

### 4 main Load Balancer Configuration

- Frontend IP Configuration
  - Public IP exposed by the load balancer
- Backend Pool
  - VMs that are connected to the load balancer
- Health Probes
  - Checks the health of the VM
    - It runs in intervals
    - Can run on TCP, HTTP, HTTPS,
    - Configurable unhealthy threashold - How many times a check should fail before marking it down(Default is 2)
    - Runs on the VM's Host
    - Allowed by default in NS
    - Originate from the same IP as the host VM
- Load Balancing rules
  - Rules connecting the frontend IP to the backend pools

### When to use Load Balancer

- Greate for internal resources
- Do not use for external resources eg Web Apps/ Web APIs
- Does not route based on path
- No Protection

### Application Gateway

- Web traffic load balancer - Load balancer with improved capabilities
- Can function as the external endpoint of the web apps
- It works with
  - VMs
  - VM Scale Sets
  - App Services
  - Kubernetes(with some hacking)
- Similar to load balancer with additional Features
  - SSL Termination
  - Autoscaling
  - Zone redundancy
  - Session affinity
  - URL based routing
  - WebSocket and HTTP/2 support
  - WAF
  - Custom error pages

### WAF

- Web Application Firewall
- Protects web apps against common attacks - Cross site scripting, SQL Injection
  Protection rules based on OWASP core Rule set
- Updates Continuously
- Works in Detection or Prevention Mode
- Many organization have their own WAF such as (Imperva, Fortinet)
- In these cases - there's no need for WAF in the application gateway

### Application Gateway SKUs

- Standard_V2 - includes all the features mentioned including WAF
- WAF_V2 - includes everything(almost double in price)

### Application Gateway Subnet

- Application Gateway is placed on its own subnet
- Often on its own VNet
- Must make sure backend resources are:
  - Accessible from application gateway subnet
  - Not accessible from anywhere

### 5 Application Gateway Configuration

- HTTP Settings
  - Set the HTTP incoming requests
- Backend Pool
  - VMs, Scale Sets and App Service that are connected to the load balancer
- Listeners
  - Receives requests on a specific port and protocol
- Load Balancing rules
  - Rules connecting the frontend IP to the backend pools

` Practical video start at 29`

## Azure SQL

- Works like any SQL Server using the same tools
- Great compactibility with on-prem SQL server
  - Depends on the exact Azure SQL Flavour
- Offers built-in security, backups, availability and more
- Flexible pricing model

### Azure SQL Flavour

- Azure SQL Database
- Elastic Pool
- Managed Instance

### Azure SQL Database

- Managed SQL Server on Azure
- Single Database on a single server
- Automatic backups, updates, scaling
- Good compactibility with on-premise
  - Not all features are supported
- Security
  - IP Firewall rules
  - Service Endpoint
  - Sql & Azure AD Authentication
  - Secure communication (TLS)
  - Data encrypted by default (TDE)
- Backups
  - Full Backup - Every 2 weeks
  - Differential backup - Every 12-24 hours
  - Transaction Log - Every 5-10 mins
- Retention Period:
  - Regular backup: 7-35 days (default is 7)
  - Long term backup: up to 19 years
- Availability
  - Backup is stored in a geo-redundancy storage
  - Active geo-replication
  - SLA: 99.9-99.995% dependent on the tiers and tools
- Compute Tiers
  - Provisioned
    - Pay for allocated resources regardless of actual use
    - Can be reserved - You can pay upfront
  - Serverless
    - Pay as you go
    - Automatically pause when not used
    - Slight delay in warming up

### Elastic Pool

- Allows storing multiple database in a single server
- Cost effective
- Purchase the compute resources you need, not the database

### Managed Instance

- Closer to the on-prem SQL Server
- Near 199% compactible with on-premise SQL
- Can be deployed to VNet
- Business model close to on-premise

### Diff. Between Azure SQL and Managed

- Does not support active geo-replication
- SLA: 99.99%
- Supports built-in functions
- Runs CLR code
- No auto scaling and tuning

` Practical video start at 007`

## Cosmos DB

- Fully managed NoSQL database
- Amazing Performance - <10ms for 99% of operation
- Globally distributed
- Fully automatic management - updates, scaling, fixes
- Multiple APIS:

  - SQL, Mongo, Gremlin, Azure Table

- It is hierarchical
- Full backup every 1-24 hours(defualt is 4)
- Retention period 20-20 days (default is 30)
- Items are divided into partitions- a logical group of items based on properties
- Partition is the basic scale unit in cosmos DB
- Make sure items are divided as evenly as possible
- Cannot be modified

## Cosmos DB Consistency Levels

- Traditionally
  - Relational DB - Strong consistency - Calls returns only after a successful commit in all replicas (High availability)
  - No SQL DB - Eventual consistency: Call returns immediately commit in replicas happens later (low latency)

c Levels
If region X updates an item and region Y reads it which data will region Y

- Strong
  - Used for mission critical data

Region Y will lag behind region X by K versions or T time

- Bounded Staleness

  - Keeps the order of the versions
  - Used for low write latency and order is important

- Session
  In a client session - Strong consistency
  - other clients - Consistent Prefix (Sometime Eventual)

## Consistent Prefix

- Keeps the order of the versions
- No guarantee of the lag size
- Used for low write latency

## Eventual

- No order guarantee
- No guarantee of the lag size
- Used for count of Retweets, Likes e.t.c

## Cosmos DB Consistency Configuration

- Configured at the account level
- Can be relaxed based on request
