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

## OCI Distributed Cloud

