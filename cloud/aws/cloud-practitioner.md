# AWS Certified Cloud Practitioner

<br/>

## Table of Content
- [I. Introduction to the Cloud](#i-introduction-to-the-cloud)
- [II. Compute in the Cloud](#ii-compute-in-the-cloud)


</br>

## I. Introduction to the Cloud

### (A) Definition

- on-demand delivery of IT resources over the internet with pay-as-you-go pricing
- support client-server models with virtual machines, databases, storage, networking, serverless
- features: pay as you go, pay on-demand, over the internet, of IT resources

#### (1) on-premise
- run in local data center
- dedicated hardware
- no cloud benefits such as elasticity or pay-as-you-go
 
#### (2) cloud-based
- run in the cloud
- use managed cloud infrastructure
- benefit from scalability, flexibility, and pay-as-you-go

#### (3) hybrid
- mix cloud and on-premises solutions
- keep legacy on-premises, and use cloud for new tasks

<br/>

### (B) Benefits

- variable expense
- economies of scale
- no capacity guessing
- speed and agility
- no physical infrastructure
- global and quick deployment

<br/>

### (C) Global Infrastructure

- geographical distribution, plus 3+ availability zones (AZ)
- AZ provides high availability and fault tolerance

<br/>

## II. Compute in the Cloud

### (A) AWS EC2 - elastic compute cloud

- provides virtual machine service, being faster, elastic and cheaper solution than on-premises
- provides on-demand computer power, handling client/server requests without managing physical servers
- pay-as-you-go, enabling operation and termination anytime without long-term commitments
- multi-tenant architecture, hypervisor isolates and allocates resource, while AWS manages hardware
- fully control over virtual server setup with OS, instance type, software and network accessibility
- supports vertical scaling by resizing CPU instance and memory based on dynamic demand

### (1) Step to run
#### (a) Launch instance
- select an Amazon Machine Image (the template that defines the operating system and initial software)
- select an instance type to decide CPU, memory, and network performance

#### (b) Connect (either one)
- use Secure Shell (SSH) to connect to Linux instances
  (key-based authentication -> via port 22 -> remote control the Linux machine)
- use Remote Desktop Protocol (RDP) to connect Windows instances
  (validate with password -> via port 3389 -> GUI panel to control)
- use AWS Systems Manager to secure access without opening ports
  (IAM for permission -> manage through Session Manager or Commands)

#### (c) Use
- Run commands and install required software
- Deploy and run applications
- Manage files, storage, and system resources


### (2) Comparison: EC2 vs. on-premises

| Aspect | On-Premises | Amazon EC2 |
|-------|------------|------------|
| Upfront cost | High hardware cost | No upfront hardware cost |
| Setup time | Takes a long time | Ready in minutes |
| Scaling | Hard to scale | Easy to scale |
| Payment | Pay even if unused | Pay only when running |


### (3) Launch EC2

| Step | Statement |
|------|-----------|
| 1 | Assign a name to the EC2 instance for identification. |
| 2 | Select an Amazon Machine Image (AMI) to define the operating system and base software. |
| 3 | Choose an instance type to determine CPU and memory capacity. |
| 4 | Select or create a key pair to enable secure access to the instance. |
| 5 | Configure network settings and allow required inbound traffic (e.g. HTTP). |
| 6 | Attach storage by configuring an EBS volume for the instance. |
| 7 | Add user data to run startup scripts and install required services. |
| 8 | Launch the instance and verify access using its public IP address. |

- *The required configurations are Amazon Machine Image (AMI), instance type, and storage.*
*An AMI is used to pre-configure the operating system and software for an EC2 instance.*


### (4) Pricing

| Pricing Option | Features | Use Cases | Restrictions |
|---------------|--------------------------|-------------|----------------|
| On-Demand | No commitment, high flexibility | Testing, learning, short-term or unpredictable workloads | Long-running, steady-state systems |
| Savings Plans | Commit to spend, flexible usage | Predictable workloads across EC2, Lambda, Fargate | Uncertain or short-lived workloads |
| Reserved Instances | Commit to instances | Steady, predictable, long-term workloads | Frequently changing instance types |
| Spot Instances | Cheapest, interruptible | Batch jobs, CI/CD, fault-tolerant processing | Databases, user-facing, stateful services |
| Capacity Reservations | Guaranteed capacity | Business-critical workloads needing assured launch | Cost-optimization-focused scenarios |
| Dedicated Hosts | Full physical server control | Compliance, licensing, hardware-level control | General-purpose workloads |
| Dedicated Instances | Hardware isolation | Isolation without server placement control | When full host control is required |

- *Spot Instances are for interruptible workloads to save money; On-Demand is for uncertain usage that needs stable, uninterrupted capacity.*

<br/>

### (B) Auto Scaling and Load Balancing

### (1) Scaling

#### (a) Scalability
- the ability of a system to handle increased workload by adding resources
- focuses on long-term growth and capacity planning
- **Scale-up** (increase instance size / add CPU and memory)

#### (b) Elasticity
- the ability to automatically adjust resources based on real-time demand
- focuses on short-term demand changes
- **Scale-out** (add instances when demand rises)
- **Scale-in** (remove instances when demand drops)

#### (c) Comparison: Scale Out vs. Scale Up

| Aspect | Scale Out (Horizontal Scaling) | Scale Up (Vertical Scaling) |
|------|-------------------------------|-----------------------------|
| Scaling method | Add more EC2 instances | Increase CPU or memory of an EC2 instance |
| Use Case | Distributable workloads (e.g. web traffic) | Workloads needing more power per machine |
| Flexibility | Different components can scale independently | Limited to a single instance |
| Fault tolerance | Higher, failure of one instance does not stop the system | Lower, relies on one instance |
| Limitation | Requires traffic distribution | Has size and hardware limits |

#### ​(d) Real-Time Scaling, Availability, and Cost Efficiency
- **Real-time scaling**<br/>
*Automatically launched or terminated EC2 instances based on real-time performance metrics.*
- **Monitoring and Scaling Triggers**<br/>
*CloudWatch collects and monitors metrics which trigger scaling actions, when predefined thresholds are reached.*
- **High Availability and Fault Tolerance**<br/>
*EC2 instances are distributed across multiple Availability Zones within a Region to remove single points of failure and improve fault tolerance.*
- **Cost-efficiency**<br/>
*Resources are provisioned only when needed, and unused instances are terminated when demand decreases, ensuring cost efficiency.*

#### (e) Auto Scaling Group Configuration

| Setting | Description | Purpose |
|--------|-------------|------------------------|
| Minimum capacity | The lowest number of EC2 instances required for the application to run | Ensures the system never scales below a safe baseline; this number of instances launches immediately when the auto scaling group is created |
| Desired capacity | The ideal number of EC2 instances needed to handle the current workload | Auto Scaling continuously attempts to maintain this number; defaults to the minimum capacity if not specified |
| Maximum capacity | The upper limit on the number of EC2 instances that can be launched | Prevents over-scaling, controls costs, and defines the scaling boundary |

<br/>


### (2) Directing Traffic with Elastic Load Balancing

##### (a) Elastic Load Balancing
- Problem: overloading EX2 instances with increasing traffic, leading to poor performance and potential service failures
- automatically distributes incoming traffic across multiple EC2 instances
- acts as a single entry point for traffic and routes requests only to healthy, available instances.
- fully managed by AWS, instead of manual patching, upgrades, failover, and maintenance

#### (b) ELB and Auto Scaling
- auto Scaling adjusts the number of EC2 instances based on demand, while ELB distributes traffic evenly across those instances.
- ELB automatically updates its routing without requiring changes to the application, when new instances are added or removed by Auto Scaling

#### (c) Benefits
- decouples frontend and backend tiers by providing a single endpoint, removing the need for services to track individual instance addresses.
- enables independent scaling of each tier, allowing frontend and backend resources to scale based on their own demand.
- improves performance by evenly distributing incoming traffic across available instances.
- prevents resource imbalance by avoiding overloaded instances and reducing idle capacity.
- enhances scalability and resilience by automatically adjusting to traffic changes without manual reconfiguration.
- simplifies operations by handling traffic routing, health checks, and fault tolerance as a managed service.

##### (d) Routing Strategies
- uses routing strategies such as Round Robin, Least Connections, IP Hash, and Least Response Time to optimize traffic distribution and reduce latency

<br/>

### (3) Messaging and Queuing

- messaging and queuing enable asynchronous communication between application components
- enable systems to continue operating smoothly even when some components are slow, busy, or temporarily unavailable

##### (a) Coupling and Architecture
- tightly coupled architectures rely on direct communication between components, so a failure in one component can cause cascading failures across the system
- Loosely coupled architectures use queues or events as intermediaries, allowing components to work independently and improving resilience and fault tolerance

#### (b) Amazon SQS (Message Queuing)
- stores messages until a consumer is ready to process them, making it ideal for buffering workloads and decoupling services

#### (c) Amazon SNS (Publish–Subscribe)
- deliver messages immediately to multiple subscribers, making it suitable for notifications, alerts, and fan-out messaging

#### (d) Event-Driven Communication
- enables event-driven architectures by routing events between services, allowing applications to scale independently and remain loosely coupled

#### (e) Architecture Impact
- move from monolithic to microservices architectures
- isolating failures and enabling independent service communication through messaging services, increasing availability and scalability

<br/> 

## III. Exploring Compute Services

### (A) Overview

### (1) Managed Compute Services
- shift more operational responsibility to AWS to manage servers and infrastructure
- Customers mainly configure the service and deploy applications
- Examples: Elastic Load Balancing, Amazon SQS, and Amazon SNS.

### (1) Serverless Computing
- remove the need to provision or manage any servers
- Customers focus entirely on application logic and code
- AWS fully manages infrastructure, scaling, availability, and maintenance

| Service Model | Customer Responsibility |
|--------------|-------------------------|
| Unmanaged | Configure OS, security patches, and network settings |
| Managed | Choose deployment options and configure environment settings |
| Fully managed | Focus only on writing and deploying code |

<br/>

### (B) AWS Lambda
- Lambda functions are invoked by events such as file uploads, data streams, or application requests
- automatically provisions the execution environment and handles scaling, availability, patching, and maintenance
- Lambda scales up or down automatically based on the number of incoming events
- The maximum execution time for a Lambda function is 15 minutes

### (1) Responsibility Model
- manages the infrastructure, execution environment, scaling, and availability, while customers focus on writing and securing their application code

### (2) Pricing and Performance
- charges only for the compute time used, and performance can be tuned by adjusting the function’s memory allocation

### (3) Runtime and Language Support
- supports multiple programming languages through managed runtimes and allows custom runtimes for unsupported languages

### (4) Integration with AWS Services
- integrates seamlessly with other AWS services, enabling fully serverless applications without managing servers

### (5) Use Cases
- file processing, request handling, real-time data processing and background jobs

### (6) Setup Procedures
- An SQS queue automatically triggers a Lambda function when a new message is added.
- Lambda function needs the correct IAM permissions to read messages from the SQS queue.

| Step | Statement |
|------|-----------|
| 1 | Create an SQS queue and send the test messages to the queue. |
| 2 | Use SQS blueprint, pre-confugures tigger and codes to create the Lambda function. |
| 3 | Assign the execution role with SQS poller policy, enable Lambda to retrieve messages from the queue. |
| 4 | the Lambda function reads messages from the SQS queue and logs message details. |
| 5 | Once messages are processed, they are automatically removed from the queue. |
| 6 | Lambda execution metrics and logs are viewed using Amazon CloudWatch. |
| 7 | CloudWatch log streams confirm that messages were successfully processed by the Lambda function. |

- Integrating SQS with Lambda enables a simple, scalable event-driven architecture where messages are processed automatically without managing servers.
- Automated photo processing uses a Lambda function, triggers, and runtimes, with no server or scaling management required.

<br/>

### (C) Containers and Orchestration

### (1) Containers
- package application code, runtime, dependencies, and configuration into a single unit
- ensures the application runs the same in development, testing, and production
- share the host OS, make it lightweight and start faster than VMs

### (2) Orchestration
- orchestration tools are used to manage deployment, scaling, and recovery for running multiple containers
- Examples: Amazon ECS (native, simple), Amazon EKS (flexible, portable)

### (3) Amazon ECR
- stores, manages and versions container images
- After ECR built, container images are pushed into it
- When deploying containers, ECS and EKS pull container images from ECR

### (4) Compute Options for running Containers

| Compute Option | Who Manages Servers | Notes |
|---------------|---------------------|-------|
| Amazon EC2 | Customer | Full control over virtual machines and infrastructure |
| AWS Fargate | AWS | Serverless option with automatic scaling |
| Fargate Compatibility | AWS | Works with both Amazon ECS and Amazon EKS |

### (5) Typical Container Workflow
| Step | Statement |
|------|-----------|
| 1 | Build a container image with application code and required dependencies. |
| 2 | Push the container image to Amazon Elastic Container Registry (ECR). |
| 3 | Choose a container orchestration service, such as Amazon ECS or Amazon EKS. |
| 4 | Select a compute option to run containers, either Amazon EC2 or AWS Fargate. |
| 5 | Deploy containers and allow the orchestration service to handle scaling and management automatically. |

