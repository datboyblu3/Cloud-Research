## Account and Access Concepts

#### Tenancy
- This is your account created for you when you sign up for Oracle Cloud services
- It is also a secure and isolated parition within OCI where you can create, organize and administer your cloud resources

#### Compartment



## OCI Architecture

#### Regions
- A region is a localized geographic area
- Oracle cloud regions are globally distributed data centers that provide secure, high performance, local environments

#### Availability Domains
- These are one or more data centers located within a region
- They are isolated from each other, fault tolerant and unlikely to fail simultaneously
- Physical infrastructure is not shared
  
#### Fault Domains
- a group of hardware and infrastructure within an availability domain.
- Each AD contains three fault domains
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

#### Routing

- **Services Gateway**: A service gateway allows traffic to and from all subnets at the time of creation; there's no mechanism to block or disable this traffic.
- **Dynamic Routing Gateway**: provides a path for private network traffic between the VCN and an on-premises network. This traffic is routed to the data center network and on to its destination.

