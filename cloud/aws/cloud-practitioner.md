review this notes:

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

### (C) Benefits

- variable expense
- economies of scale
- no capacity guessing
- speed and agility
- no physical infrastructure
- global and quick deployment

### (D) Global Infrastructure

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

#### (1) Step to run

(a) Launch instance
- select an Amazon Machine Image (the template that defines the operating system and initial software)
- select an instance type to decide CPU, memory, and network performance

(b) Connect (either one)
- use Secure Shell (SSH) to connect to Linux instances
  (key-based authentication -> via port 22 -> remote control the Linux machine)
- use Remote Desktop Protocol (RDP) to connect Windows instances
  (validate with password -> via port 3389 -> GUI panel to control)
- use AWS Systems Manager to secure access without opening ports
  (IAM for permission -> manage through Session Manager or Commands)

(c) Use
- Run commands and install required software
- Deploy and run applications
- Manage files, storage, and system resources


#### (2) Comparison: EC2 vs. on-premises

| Aspect | On-Premises | Amazon EC2 |
|-------|------------|------------|
| Upfront cost | High hardware cost | No upfront hardware cost |
| Setup time | Takes a long time | Ready in minutes |
| Scaling | Hard to scale | Easy to scale |
| Payment | Pay even if unused | Pay only when running |


#### (3) Launch EC2

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

*The required configurations are Amazon Machine Image (AMI), instance type, and storage.*
*An AMI is used to pre-configure the operating system and software for an EC2 instance.*

#### (4) Pricing

| Pricing Option | Features | Use Cases | Restrictions |
|---------------|--------------------------|-------------|----------------|
| On-Demand | No commitment, high flexibility | Testing, learning, short-term or unpredictable workloads | Long-running, steady-state systems |
| Savings Plans | Commit to spend, flexible usage | Predictable workloads across EC2, Lambda, Fargate | Uncertain or short-lived workloads |
| Reserved Instances | Commit to instances | Steady, predictable, long-term workloads | Frequently changing instance types |
| Spot Instances | Cheapest, interruptible | Batch jobs, CI/CD, fault-tolerant processing | Databases, user-facing, stateful services |
| Capacity Reservations | Guaranteed capacity | Business-critical workloads needing assured launch | Cost-optimization-focused scenarios |
| Dedicated Hosts | Full physical server control | Compliance, licensing, hardware-level control | General-purpose workloads |
| Dedicated Instances | Hardware isolation | Isolation without server placement control | When full host control is required |

*Spot Instances are for interruptible workloads to save money; On-Demand is for uncertain usage that needs stable, uninterrupted capacity.*


### (B) Auto Scaling and Load Balancing

#### (1) Scaling

(a) Scalability
- the ability of a system to handle increased workload by adding resources
- focuses on long-term growth and capacity planning
- **Scale-up** (increase instance size / add CPU and memory)

(b) Elasticity
- the ability to automatically adjust resources based on real-time demand
- focuses on short-term demand changes
- **Scale-out** (add instances when demand rises)
- **Scale-in** (remove instances when demand drops)

(c) Comparison: Scale Out vs. Scale Up
| Aspect | Scale Out (Horizontal Scaling) | Scale Up (Vertical Scaling) |
|------|-------------------------------|-----------------------------|
| Scaling method | Add more EC2 instances | Increase CPU or memory of an EC2 instance |
| Use Case | Distributable workloads (e.g. web traffic) | Workloads needing more power per machine |
| Flexibility | Different components can scale independently | Limited to a single instance |
| Fault tolerance | Higher, failure of one instance does not stop the system | Lower, relies on one instance |
| Limitation | Requires traffic distribution | Has size and hardware limits |

​(d) Real-Time Scaling, Availability, and Cost Efficiency
- **Real-time scaling**
*automatically launched or terminated EC2 instances based on real-time performance metrics.*
- **Monitoring and Scaling Triggers**
*CloudWatch collects and monitors metrics which trigger scaling actions, when predefined thresholds are reached.*
- **High Availability and Fault Tolerance**
*EC2 instances are distributed across multiple Availability Zones within a Region to remove single points of failure and improve fault tolerance.*
- **Cost-efficiency**
*Resources are provisioned only when needed, and unused instances are terminated when demand decreases, ensuring cost efficiency.*

(e) Auto Scaling Group Configuration
| Setting | Description | Purpose |
|--------|-------------|------------------------|
| Minimum capacity | The lowest number of EC2 instances required for the application to run | Ensures the system never scales below a safe baseline; this number of instances launches immediately when the auto scaling group is created |
| Desired capacity | The ideal number of EC2 instances needed to handle the current workload | Auto Scaling continuously attempts to maintain this number; defaults to the minimum capacity if not specified |
| Maximum capacity | The upper limit on the number of EC2 instances that can be launched | Prevents over-scaling, controls costs, and defines the scaling boundary |


<br/>
