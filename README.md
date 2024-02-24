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

``` Practical videos starts at video 15 in azure compute folder ```

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
- Total Seconds: 9m * 1.5s = 13.5m secs
- Total GB/Sec = 13.5m * 0.8 = 10.8m - 400K free grant = 10.4m GB/sec
- Payment for execution time: 10.4m * 0.000016$ = 1.66.4$
- Payment for executions: 9m-1m free grant = 8m * 0.3$/m = 1.6$
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
- vCPU cost: 123.37 * 2 = 246.74$
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

``` Pratical videos starts at 006```