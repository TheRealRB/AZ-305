##Virtual Machines
- VM Sizing:
 - B burstable
 - D general
 - E memory
 - F compute
 - M large memory
 - L storage
 - N GPU
  
 Standard_D2s_v5 = (D)General purpose + 2 vCPUs + (s)premium disk + (v5)hardware generation
  
  - VMSS - Virtual Machine Scale Sets - groups of identical, load-balanced VMs. Can automatically scale out or in based on demand of schedules.
  - VM Availability Sets - improve your resiliency inside a region. Reduce the chance that all VMs are affects by maintenance or failure. Availability Sets don't add cost. Instead you pay for the VMs.

- Azure Container Instances are a platform as a service (PaaS) offering. You upload your containers and the service runs them for you.
- Azure Container Apps remove the container management overheaed (PaaS) and also include built-in load balancing and scaling.
- Azure Kubernetes Service (AKS) is a container orchestration service that manages the lifecycle of containers. Where you're deploying a large number of containers (a fleet) AKS can make fleet management simpler and more efficient.
  
- Azure Functions - no need to keep resources running in order for your app to function. An event wakes the function. Functions are commonly used when you need to perform work in response to an event (REST request). Functions scale automatically. Can be stateless (default) or stateful (Durable Functions).
  
- Azure AI services provides prebuilt capabilities for common AI scenarios.
- Agentic AI patterns - combine an AI model with instructions, context, and tool use to complete multistep goals.
- Azure Machine Learning - when you need to build, train, and manage custom machine learning models.
- IoT and Edge services
  - Azure IoT Hub enables secure, bi-directional communication between cloud services and IoT devices.
  - Azure IoT Central provides simplified software as a service (SaaS) IoT platforms for solution builders.
  - Azure IoT Edge extends cloud capabilities to edge devices so some workloads can run closer to where the data is stored.

# Azure Storage Services
- Must have a unique namespace across Azure (3-24 characters in length and may contain numbers and lower case letters only)
- Standard general-purpose v2 - blobs, file shares, queues, and tables. Can use all redundancy options: LRS, GRS, RA-GRS, ZRS, GZRS, RA-GZRS
- Premium block blobs - blob storage including Data Lake Storage. Remember Data Lake Storage is not a type of storage, it's essentially blob storage + hierarchical namespace for low latency fast analytics. Premium can only use LRS and ZRS redundancy.
- Premium file shares - high-scale or high-performance file share for applications. Supports both SMB and NFS shares.  LRS & ZRS
- Premium page blobs - page blobs only. LRS only.
- Endpoint URL formats for storage services:
  blob storage: *.blob.core.windows.net
  Data Lake Gen 2: *.dfs.core.windows.net
  Azure Files: *.file.core.windows.net
  Queue Storage: *.queue.core.windows.net
  Table Storage: *.table.core.windows.net

- LRS provides three copies of your data in a single zone (datacenter) and gives 11 nines of uptime over a year.
- ZRS provides three copies of your data across three zones (datacenters) and provides 12 nines of uptime over a year.
- GRS uses LRS in both regions
- GZRS uses ZRS in the primary region and LRS in the secondary region. By default, data in the secondary region is not readable until a failover occurs. Data is replicated to the secondary region asyncronously.
- Azure RPO is 15 minutes so there can be some data loss during an event and failover.
  
- Core Data Services:
 - Azure Files
 - Azure Queues - millions of messages. Queues are accessed by authenticated HTTP/HTTPS calls. Supports up to 64 KB size.
 - Azure Disks - virtualized disk block level volumes for Azure VMs.
 - Azure Tables - NoSQL store for larg amounts of stuctured, non-relational data, available through authenticated calls from cloud and hybrid environments.
   
- Azure data migration options:
 1) Azure Migrate. Single portal to assess and migration. Real time migration hub. Server, Database, Web app, ISV tool integration.
 2) Azure Data Box. Offline bulk data transfer. Ship a secure storage device with up to 80TB.
  
- Azure file movement options:
 1) AzCopy. One-way sync, copy between accounts, upload and download files.
 2) Storage Explorer. GUI for Win/Mac/Lin. Uses AzCopy on the backend. Manage blobs and files.
 3) Azure File Sync. Bi-dir sync, cloud tiering, SMB, NFS, FTPS protocols, multisite caching. Installed on Window server.



 
