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

#### (1) cloud-based
- run in local data center
- dedicate hardware, low latency
- no cloud benefits
 
#### (2) on-premise
- run in the cloud
- fully migrate legacy to new build cloud solution
- cloud benefit (scalable, flexible, pay-as-you-go)

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

#### (1) Step to run EC2

(a) Launch instance
- select an Amazon Machine Image (the template that defines the operating system and initial software)
- select an instance type to decide CPU, memory, and network performance

(b) Connect (either one)
- use Secure Shell (SSH) to connect to Linux instances
  (key-based authentication -> via port 22 -> remote control the Linux machine)
- use Remote Desktop Protocol (ROP) to connect Windows instances
  (validate with password -> via port 3389 -> GUI panel to control)
- use AWS Systems Manager to secure access without opening ports
  (IAM for permission -> manage through Session Manager or Commands)

(c) Use
- Run commands and install required software
- Deploy and run applications
- Manage files, storage, and system resources


#### (2) Comparison between EC2 and on-premises

| Aspect | On-Premises | Amazon EC2 |
|-------|------------|------------|
| Upfront cost | High hardware cost | No upfront hardware cost |
| Setup time | Takes a long time | Ready in minutes |
| Scaling | Hard to scale | Easy to scale |
| Payment | Pay even if unused | Pay only when running |
