# Notes from both Oracle's Official Course and ExamPro OCI YouTubve Video

## Account and Access Concepts

#### Tenancy
- This is your account created for you when you sign up for Oracle Cloud services
- It is also a secure and isolated parition within OCI where you can create, organize and administer your cloud resources

#### Compartment

## OCI Architecture

#### Regions
- A region is a localized geographic area that has many datacenters aka *Availability Domains*
- Oracle cloud regions are globally distributed data centers that provide secure, high performance, local environments
- Three kinds of regions:
  - Commerical: any customer can launch resources in these regions
  - Government: Only governments can launch resources in these regions
  - Azure Connected: Some commercial regions are connected to Azure
- A region can be multiple places in the world 

#### Availability Domains
- These are one or more data centers located within a region
- They are isolated from each other, fault tolerant and unlikely to fail simultaneously
- Need to be close enough to provide low-latency
- Physical infrastructure is not shared
- Is what OCI calls a datacenter
- A region will generall contain 3 datacenters (ADs)
  
#### Fault Domains
- a group of hardware and infrastructure within an availability domain.
- They are logical datacents - a virtual/abstrct datacenter within a physical datacenters
- Each AD contains three fault domains
- Primary purpose is to isolate groupings of hardware within a datacenter so they don't share a single point of failure
- Allow you to distribute your instances/applications so that the instances are not on the same phyiscal hardware within a single AD
- This offers redudancy
- Instances within a fault domain are sandboxed from each other

![fault_domains2](https://github.com/datboyblu3/Cloud-Research/assets/95729902/22e95f8a-b465-4651-9f79-e3b23cfcecf0)


#### Realm
- A set of regions that share the same characteristics

## 4. Identity and Access Management

### What is OCI AIM?
- IAM = Identity and Access Management Service
- Fine-grained Access Control
- AuthN - Who are you?
- AuthZ - What permissions do you have?

#### Identity Domains
- An identity domain represents a user population in OCI and associated configurations and security settings
- First you create your Identity domain, then create your users and groups, write policies to those users and groups, the policies are scoped to a tenancy 
- A container for your user and groups

#### OCID
- A unique identifier for all your resources, Oracle Cloud ID
- Automatically provided
- Syntax: ocid1.RESOURCE TYPE.REALM.REGION.FUTURE USE.UNIQUE ID

#### Compartment
- A logical concstruct that is a collection of related resources
- You can create your own compartment within. You create these for isolation and network control
- Best practice is to create dedicated compartments to isolate resources
- Each resource you create belongs to a single compartment
- Resources do not have to be in the same compartment to interact with each other, but how?
- Via using the virtual cloud network
- Resources can be moved from one compartment to another
- They are global constructs - resources from multiple regions can in the same compartment
- They are available in every region you have access to
- Compartments allows for 6 levels of nesting, this helps to keep your design cealn

#### Principal
- These are IAM entities that are allowed to interact with OCI resources
- Two types are IAM Users and Resource Principals
- Policies can be attached to a compartment (only adheres to resources within that compartment) or the tenancy (everything within the Tenancy)

#### Tenancy Setup
- Best practices:
  - is to have an OCI admin to perform daily tasks
  - This OCI admin should run this account, not the Tenancy admin
  - Create dedicated compartments to isolate resources
  - enforce the use of MFA

- OCI Admin should scope policies to all compartments

## 5. Networking

### Virtual Cloud Networking - VCN
 - A private software, defined network created in Oracle cloud
 - Created to communicate with private, internal Oracle sources

**Concepts to know** :
- **Internet Gateway**: an optional gateway you can add to your VCN to enable direct connectivity to the internet.
- **NAT Gateway**: a networking technique commonly used to give an entire private network access to the internet without assigning each host a public IPv4 address. The hosts can initiate connections to the internet and receive responses, but not receive inbound connections initiated from the internet

#### VCN Routing
- **Services Gateway**: A service gateway allows traffic to and from all subnets at the time of creation; there's no mechanism to block or disable this traffic.
- **Dynamic Routing Gateway**: provides a path for private network traffic between the VCN and an on-premises network. This traffic is routed to the data center network and on to its destination.

#### VCN Security
- Security lists can be fw rules associated with a subnet and applied to all instances in a subnet
- Security lists consists of rules that specify the type of traffic allowed in/out of the subnet
- Network Security Group (NSG): similar to security lists but apply to network interface cards in a single VCN. Can either be the src or dest in the rules
- Because NGS apply to individual VNICS, you can have two instances in a single subnet and they can have different security constructs

#### Load Balancers
- Use load balancers to achieve high availability and scalability
- Layer 7 LB, HTTP/S
- 
## 6. Compute

**Virtual Machine**
  - Shared, multi tenants
  - Strong security, isolated hosts
    
**Bare Metal**
 - You get a full machine/server 100% dedicated to you
 
**Dedicated Hosts**
  - Are also 100% dedicated to you
  - Can run own VMs,
  - VMs are privately owned

### Capitval vs Operational Expenditure

**CAPEX (Capital Expenditure)**

- Buidlings
- Vehicles
- Hardware
- Equipment
- Land

**OPEX (Operational Expenditure)**

- Products
- Business
- Systems

**Containers**

- docker deamon is the name of the software layer that lets you run multiple containers
- containers share the same underlying OS, they're more efficient than multiple VMs
- Multiple apps can run side by side without being limited to the same OS requirements and will not cause conflicts during resource sharing

**Functions**

- a managed VMs running managed containers
- known as *Serverless Compute*
- You upload a piece of code, choosing the amount of memory and duration
- only responsible for code + data
- cost effective, only pay for the time code is running, VMs only run when there is code to be executed
- Cold starts is a side-effect of this setup

### OCI Concepts

**Console**

The console is the simple web-based user interface you can use to access and manage Oracle Cloud Infrastructure

**Tenancy**

Oracle creates a tenancy for your company, which is a secure and isolated partition within OCI where you can create, organize and administer your cloud resources

**Compartments**

- A logical collection of related resources that can be accessed only by certain groups that have been given permission by an admin

- A *root compartment* is created when you signup, it holds all of your cloud resources

- can nest compartments six levels deep
- add/delete compartments whenever
- not region specific, can group resources cross region
- resources can be easliy moved to other compartments
- compartment resources can interact with each other
- can apply policies to compartment to determine user access
- can associate a compartment to a budget for cost analysis

**Application Program Interface (API)**
- A way to interact with cloud services programatically

**Command Line Interface**
- Allows you to access the API via the shell terminal program

**CloudShell**
- A web browser-based terminal accessible from the Oracle Cloud Console. Cloud Shell is free to use and provides access to a Linux shell, with a pre-authenticated Oracle Cloud Infrastructure CLI

**Software Development Kit**
- A set of programming librarues available in common languages to interact with Oracle Cloud Services

## Core Services

### Computing Services

**Virtual Machines**
- A multi-tenant serving running a hypervisor layer. Share the ecost with other customers so you save

**Container Engines**
- Docker as Service. Allows you to run docker containers on a virtual machine

**Functions**
- Serverless compute. Code is designed to run for a short a period of time and you choose a managed container with runtime

**Dedicated Virtual Hosts**
- A single tenant server that is running a hypervisor layer where you can run multiple 

**Bare Metal**
- A dedicated server that has no hypervisor layer
- Allows you to provide your applications with direct access to the processor and memroy resources of the underlying server
- Is suited for specialized workloads where hypervisor would hinder performance

### Storage Services

**Block Volume**
- Similar to a local virtual hard drive.
- Either HDD or SSD
- Data is split into evenly split blocks directly accessed by the OS
- Supports only a single write volume
- Multiple VMs requires multiple block volumes - hard to share between VMs
- Protocols in use are FC, iSCSI
- Most expensive at scale

**Local NVMe**
- Non-Volatile-Memory-Express, a transfer protocol for SSD that allows the drives to operate very efficiently

**File Storage**
- Uses a file system NSFv3 allowing multiple connections to the same storage device at the same time
- File is stored with data and metadata
- Multiple connections via a network share
- Supports multiple reads, writing locks the file
- Uses NFS, SMB etc

**Object Storage**
- Serverless storage
- Upload many files
- Scales without worrying about running out of space or data loss
- Object is stored with data, metadata and Unique ID
- Scales with limited no file limit or storage limit
- Supports multiple reads and writes (no locks)
- Accessed over the internet
- Protocols: HTTP/S, API
- Least expensive at scale

**Archive Storage**
- Long-term cold storage
- Files you need to keep around for years that you infrequently need to access at a fraction of the storage cost

### Networking Services

<img width="487" alt="Screenshot 2023-12-17 at 10 13 55 AM" src="https://github.com/datboyblu3/Cloud-Research/assets/95729902/81342813-1afc-41d5-ba9b-c2b59a3917b7">

In this diagram, CA-TORONTO-1 will be the Region

Virtual Firewall Options:
- Security Rules
- Network Security Groups
- Security Lists
  
<img width="537" alt="Screenshot 2023-12-17 at 10 40 42 AM" src="https://github.com/datboyblu3/Cloud-Research/assets/95729902/51974a67-81f9-4a15-9f05-fa44c50cfe37">

**Service Gateways**
- A secure tunnel that keeps traffic within the OCI Network

**NAT Gateway**
- Let resources in a private subnet reach the internet

**IPSec VPN**
- A secure connection to your on-prem to Oracle Cloud

**Fast Connect**
- A dedicated secure connection to your on-prem to Oracle Cloud

**Dynamic Routing Gateway**
- A virtual router that provides a path for private traffic between your VCN and outside network

**VCN Peering**
- Create a network connection between VCNs

### Virtual Cloud Networks and Subnets

A VCN is a logically isolated section of the OCI Cloud where you can launch OCI resources. You choose a range of IPs using CIDR Range

CIDR Range of 10.0.0.0/16 = 65,536 IPs

Subnets need to have a smaller CIDR range than the VCNs

### Virtual Network Interface Card

Enables an instance (server) to connect to a VCN and determines how the instance (server) connects with endpoints inside and outside the VCN.

Without the VCIN, your instance (server) would not be able to communicate with the internet or other network cloud services.

### Virtual Firewall Options

Two virtual firewall features are available that use security rules to control traffic at the packet level. They are:

**1. Security Lists(SLs)**
-  Associated with subnets and the security rules apply to VCINs in those subnets

**2. Network Security Groups(NSGs)**
- New virtual firewall feature designed for application components that have different security postures.
- NSGs are supported only for specific services
- Are directly associated with VCINs, regardless of subnet

### Database Services

**VM DB Systems**
- A virtual machien running a managed Oracle Database Instance
- Uses Block Storage

**VM BM Systems**
- A Bare Metal machine running a managed Oracle Database Instance
- Uses Fast Local Storage

**Oracle RAC**
- Oracle Databases running as a cluster. Shares the same disk but different instances running on different nodes
- If a node fails, connection fails over to another node
- Highly Available

**Exadata DB Systems**
- Exadata is a pre-configured combination of hardware and software that provides an infrastructure for running Oracle Database
- Specalized Infrastructure

**Autonomous**
- Automatically patches, upgrades and self-healing bad data
- Highly available by default, secure by default
- Shared/Dedicated
- Fully managed

#### DB Systems Database Options

- With Oracle DB Systems you choose your Availability Domain and Shape Type
- With MySQL DB Systems, you choose the AD, Fault Domain and Shape Type

#### Autonomous Database Options - Workload Types

**OLAP**
- Data Warehouse
- Configures the database for a decision support or data warehouse workload, with a bias towards large data scanning operations
- Reporting, analytics, large and infrequent queries

**OLTP**
- Transaction Processing
- Configures the database for a transactional workload with a bias towards high volumes of a random data access

**Shared Infrastructure**
- Multi-tenant
- Run Autonmous Database on shared Exadata infrastructure

### Oracle NoSQL

- Oracle NoSQL Database is a key/value store

Use Oracle NoSQL when...
- produce and consime data at high volume and velocity
- require instanteous response time to match user expectations
- developed with continuously evolving data models
- scale on-demand based on the dynamic workloads

### Cloud Native Services

- Oracle API Gateway. A comprehensive platform for managing, delivering, and securing Web APIs
- Oracle Streaming. Inget and store continuous, high-volume data streams and prcess them in real-time.
- Oracle Kubernetes Container Engine. A managed service to run a Kubernetes Cluster
- Oracle Registry. A repository for your docker containers
- Oracle Notifications. A fully managed publish-subscribe service for reliable and scalable message delivery.
- Oracle Integrations. A service to connect on-premise, third party to your OCI with premade adapaters for easy application integration.
