# Cloud Adoption Framework for Azure
- contains 8 methodologies
 1) Strategy
 2) Plan
 3) Ready
 4) Migrate
 5) Innovate
 6) Govern
 7) Manage
 8) Secure
  
- RAMP model skills (Ready, Administer, Monitor, Protect)
  
Assess code to identify compatibility and modernization opportuntities: AppCAT for .NET and Java applications.
  
 1) Set up your Azure environment
 2) Define a cloud operating model
  1) Centralized cloud operating model - a single team is responsible for governance, security, and operations across the entire cloud estate and all workloads. Ideal for small organizations, startups, or highly regulated. Can be a bottle at scale.
  2) Shared management operating model - responsbilities are divided between platform teams and workload teams. Ideal for mid-size and enterprise organizations; highly effective in hybrid or multicloud environments.
  3) Decentralized cloud operating model - each team owns its platform landing zone and manages its workloads independently. Ideal for highly skilled teams in startups or innovation programs.
 3) Implement landing zones
 4) Develop necessary skills
 5) Avoid antipatterns
  
- Migrate
 1) Plan migration
 2) Prepare workloads for the cloud
 3) Execute migrations
 4) Optimize workloads after migration
 5) Decomission source workloads

# Govern Methodology
 1) Build a team
 2) Assess cloud risks
 3) Document cloud governance policies
 4) Enforce cloud governance policies
 5) Monitor cloud governance


# RAMP (Ready, Administer, Monitor, Protect)

## Ready your Azure cloud operations
 1) Identify management responsibilities
 2) Establish operations teams
 3) Document operational procedures
 4) Manage daily operations
 5) Improve continuously

## Administer Azure cloud estate
 1) Define administrative scope. Determine responsibilities based on your deployment model (IaaS, PaaS, Saas, on-prem)
 2) Control changes. Implement formal change requests using ticketing tools, assess risk levels with approval workflows, standardize deployment procedures.
 3) Secure your environment. Entra ID for identity, RBAC with least privilege, enforce secure configurations with infrastructure as code.
 4) Maintain compliance. Map governance policies to operational processes using Azure Policy definitions aligned with standards like ISO 27001 and NIST SP 800-53.
 5) Govern data. Classify data using Microsoft Purview, control residency through region selection, isolate workloads through management groups. Implement access controls and deletion protection.
 6) Control costs. Use Microsoft Cost Management to monitor spending centrally and per workload. Provide billing access to teams and implement optimization practices.
 7) Manage code and runtime. Direct teams to follow Well-Architected Framework's Operational Excellence checklist for code management, testing, and deployment practices.
 8) Manage resources. Limit portal deployments to non-production, use infrastructure as code with Bicept or Terraform, and implement CI/CD pipelines. Control configuration drift and resource sprawl through governance.
 9) Handle relocations. Evaluate drivers like compliance or user proximity, assess risks including downtime, calculate costs, and use Azure relaction guidance when justified.
 10) Maintain operating systems. Automate VM maintenance, implement updates through Azure update management, and monitor using Change Tracking and Machine Configuration services.

## Monitor your Azure cloud estate
 1) Define monitoring scope
 2) Plan monitoring strategy
 3) Design monitoring solution
 4) Configure comprehensive monitoring
 5) Set up alerting
 6) Create visualizations

## Protect your cloud estate
 1) Ensure reliability
 2) Protect data
 3) Build resilient applications
 4) Deploy redundant infrastructure
 5) Plan business continuity
 6) Operate security
 7) Handle security incidents

# Secure
 - Use security guidance provided by Microsoft
  1) Cloud Adoption Framework Secure methodology
  2) Azure Well-Architected Framework security guidance
  3) Microsoft cloud security benchmark
  4) Zero Trust guidance

 - Use the CIA Triad model
  1) Confidentiality
  2) Integrity
  3) Availability

  
# Azure Well-Architected Framework
- A set of guiding tenets to build high-quality solutions on Azure
  
- The five pillars of AWAF
1) Reliability
2) Security
3) Cost Optimization
4) Operational Excellence
5) Performance Efficiency
  
# Design for governance
- Azure scopes
 1) Tenant Root Group
 2) Management Group
 3) Subscription
 4) Resource groups
 5) Resources  
  
## Management groups
 - can be used to aggregate policy and initiative assignments via Azure Policy.
 - Supports up to six levels of depth; not including root tenant or subscription level
 - RBAC authorization is not not enabled by default at MG level.
 - by default new subscriptions are placed under the root management group.
 - consider a top level MG to support common platform policy and Azure role assignments across the entire organization.
 - keep the MG hierarchy reasonably flat
 - consider an organizational or departmental structure (follow the business structure)
 - consider a geographical structure
 - consider a production MG
 - consider a sandbox MG
 - consider isolating sensitive information
  
## Subscriptions
 - can provide separate billing environments (prod, dev, uat, qa)
 - policies for individual subscriptions can help satisfy different compliance standards
 - you can organzie specialized workoloads to scale beyong the limits of an existing subscription
 - by using subscriptions, you can manage and track costs for your organizational structure
 - treat subscriptions as a democratized unit of managment
 - group subscriptions together under management groups
 - consider a dedicated shared services subscription  (Recall Sheridan/Envision CORE services)
 - consider subscription scale limits. This way you can avoid resource limits. Large, specialized workloads like high-performance computing, IoT, SAP are all better suited to use separate subscriptions.
 - consider admnistrative management
 - consider how to assign Azure policies.
 - consider network topologies (e.g. virtual networks can't be shared across subscriptions; they can be connected via peering)
 - consider making subscription owners aware of their roles and responsibilities

## Resource Groups
 - logical containers into which Azure resources are deployed and managed
 - organize resources by life cycle so all resources can be created or deleted at the same time
 - place resources of similar usage, type, or location in logical groups
 - use resource locks to protect individual resources from deletion or change
 - resource groups have their own location (region) assigned. This region is where the metadata is stored
 - if the resource group's region is down you can't update resources in the resource group because the metadata is unavailble.
 - resources in the resource group can be in different regions
 - resources can be moved between resource groups with some exceptions
 - a resource can connect to resources in other resource groups. e.g. a web app that connects to a database in a different resouce group.
 - you can add a resource or remove a resource from a resource group at any time.
 - resource groups can't be nested
 - each resource must be in one, and only one, resource group.
 - resource groups can't be renamed
  
 ### Considerations
 - consider group by type
 - consider group by app
 - consider group by department, location (region), and group by billing
 - consider resource life cycle
 - consider administrative overhead
 - consider resource access control
 - consider compliance requirements
  
## Resource Tags
 - 50 tags max per resource
 - name-value pair. one to one relationship. (Cost Center = 10200)
 - resource tags can be added, modified, and deleted. These actions can be done with PowerShell, Azure CLI, ARM templates, REST API, or Azure Portal
 - tags can be applied to a resource group. However, tags applied to a resource group aren't inherited.
 - consider your organization's taxonomy
 - consider whether you need IT-aligned or business-aligned tagging
 - resource tags generally fall into fix categories:
  1) functional
  2) classification
  3) accounting
  4) partnership
  5) purpose
 - consider using Azure Policy to apply tags and enforce tagging rules and conventions
 - consider which resources require tagging
   
## Azure Policy
 - groups of policies are called initiatives.
 - Azure Policy comes with many built-in policy and initiative definitions
 - policies are inherited down the hierarchy
 - policy evaluates all resources in Azure and Arc-enabled resources (Arc-enabled resources are those outside of Azure that are represented through Arc servers. e.g. AWS resources, on-prem servers)
 - policy highlights non-compliant resources
 - policy can block non-compliant resources from being created and also remediate non-compliant resources.
 - policy integrates with Azure Pipeplines by applying predeployment and post-deployment policies.
 - consider using Azure Policy compliance dashboard
 - consider when Azure Policy evaluates resoures. Triggers for evaluation:
  1) a resource is created, deleted, or updated within a policy scope
  2) a policy or initiative is newly assigned to a scope
  3) an assigned policy or initiative for a scope is updated
  4) the standard compliance evaluation cycle (occurs once every 24 hours)
 - consider how to handle a noncompliant resource
  1) deny changes
  2) log changes
  3) alter the resource before or after the change
  4) deploy related compliant resources
 - consider when to automatically remediate noncompliant resources (think tagging)
 - consider how Azure Policy is different from role-based access control (RBAC)
  
## Role-based access control (RBAC)
 - RBAC is an 'allow model' meaning RBAC allows the user to perform the actions associated with the role.
 - consider the highest scope level for each requirement
 - consider the access needs for each user
 - consider adding roles to groups, and not to users
 - consider when to use Azure policies
 - consider when to create a custom role
 - consider how to resolve overlapping role assignments
   
# Azure Landing Zones
- an Azure landing zone consists of a platform landing zone and one or more application landing zones. The platform landing zone hosts shared servcies (identity, connectivity, and management subscriptions) managed by a central team.
- Azure policies are associated with landing zones to ensure continued compliance with the organizational platform.
- landing zones are pre-provisioned through code (IaC; bicep, terraform)
- Azure landing zone IaC accelerator is the recommended way deploy. It uses bicep or Terraform via Azure Verified Modules (AVM) to automate deployment.
- consider using landing zones through code (IaC)
- consider using the accelerator
- consider focusing on your apps
- consider using Azure native platform services and capabilities
- consider scoping for both migrations and green field situations
- consider transitioning existing architectures to Azure landing zones
  
# Identity and Access Management (IAM)
- Entra B2B (Business to Business)
  1) invite guest users to collaborate with your Entra ID users.
  2) guest users get guest profiles in your Entra ID directory. Guest accounts are annotated as guests.
  3) can be added to same groups as your Entra users
  4) authenticated by their company's IAM; not yours
  5) you can use your own (single) branding on your UI
- Entra External ID (formerly Azure AD B2C)
  1) separate Entra ID directory / Tenant (separate from your enterprise/corporate Entra ID; you manage both)
  2) not visible to your main Entra ID users
  3) branding is fully customizable per app or org

# Conditional Access
- use to allow or deny access to resources
- MFA supports granular control. You can use MFA selectively and for certain users only
- Entra ID allows named locations to be used with app policies to control access. Named locations can be known networks or geographic locations
- can restrict to client apps only
- untrusted sources can be blocked, such as sources from an unknown or unexpected location
- report-only mode lets admins evaluate the impact before enabling the settings
- The What If tool helps you plan and troubleshoot Conditional Access policies
- Requires a P1 or P2 license or Business Premium license
- consider policies to handle compromised accounts:
  1) require all users to use MFA
  2) require a password change for users who are high-risk
  3) require MFA for users with medium or high sign-in risk
- can use to block all users from signing in to the tenant; useful during migrations or upgrades
- can block legacy authentication protocols
- consider using the Conditional Access Optimization Agent: an AI-powered agent that monitors policy gaps and recommends fixes. Requires P1 license + Security Copilot SCUs.
  
# Identity Protection
- identity protection can identify risk signals, which conditional access can use to make decisions, and identity protection can forward the risk data to your SIEM for investigation
- consider setting the user risk policy level to HIGH, per Microsoft recommendations
- consider setting the sign-in risk policy level to MEDIUM and Above per Microsoft, as this setting supports Identity Protection self-remediation options. These are less-impactful compared to blocking users.
  
# Access Review
- Entra access review is a planned review of the access needs, rights, and history of user access
- mitigate risk by protecting, monitoring, and auditing access to critical assets
- verify group memberships that are syncronized to Entra ID, or created in Entra ID / M365
- check access packages (bundled app access to make provisioning easier)
  
# Service Principals for Applications
- user principal (user) & service principal (app)
- application object is an AD object that defines the appliation and its details such as authentication method(s)
- an app can have at most, one app object, which is registered in a home direct.
- an app can have many service principals.
- a service principal for an app is the instance of the app. Service Principals are simliar to user accounts and the app runs under the SP account.
- three types of service principals
  1) application
  2) managed identity - Azure manages the credentials
  3) Legacy
- a service principal must be created in each tenant where the app will be used
- you can create a service principal object using Azure PowerShell, CLI, Graph, and other tools.
  
# Managed Identities
- free of charge
- automatically rotates and manages credentials
- you can assign RBAC with the managed identity account
- two types:
  1) system-assigned
  2) user-assigned
- can be used to access key vault during app runtime
  
# Key Vault
  1) manage secrets
  2) manage keys
  3) manage certificates
- Standard Tier - encrypt with software key
- Premium Tier - encrypt with hardware security module (HSM) protected keys
- logged and monitored
- policy can restrict secret access
- consider using separate key vaults. grouping secrets into the same vault increases the blast radius of a security event.
- consider using soft delete to roll back if accidentily deleted of the key vault
- consider using purge protection - protect against deletion by a malicious insider.
  
# Azure Monitor data sources
- common monitoring platform to view, analyze, and work with data gathered from your resources
 1) Azure monitor logs - collect and organize data from resource
 2) Azure monitor metrics - capture numerical data from monitored resources and stores the results in a time-organized database.
- analyze logs with log queries
- metrics support near-real-time scenarios like alerting and responding to critical issues
- monitoring data can be sent to other locations for tracking and reporting
- sources of monitoring can be organized into tiers starting from the highest tiers for apps and lower tiers being the components of Azure platform.
- Azure collects data using Data Collection Rules (DCRs)
- Azure Monitor Agent (AMA) uses DCRs to collect:
 1) windows events
 2) performance counters
 3) syslog
 4) IIS logs
 5) custom logs (text and JSON)
- Kusto Query Language (KQL) is used to analyze your collected data
- consider setting up alerts based on logs and metrics data
- create DCRs and assign them to your VM and hybrid machines using resource association. Use Azure Policy to enforce DCR assignment at scale.
- use Metrics Explorer to analyze metrics interactively.
  
# Azure Monitor logs (Log Analytics) workspaces
- data in Azure Monitor Logs workspaces is organized into tables.
- configure billing and retention for each workspace; use fixed daily rates, or pay-as-you-go with an optional daily cap.
- use RBAC to control users and groups with least security
- workspaces are hosted on physical clusters. clusters are (by default) automatically created and managed. Dedicated clusters are available for specific requirements such as Customer Lockbox or CMK encryption.
  
# Azure Workbooks and Azure Insights
- combine multiple data sources into a unified interactive experience
- transform ingested data to provide insights into the availability, performance, usage, and overall health of components
- analyze performance logs of VMs to identify high CPU or low memory instances
- Azure Insights provides customized monitoring for particular apps and services
- Azure Insights collects and analyzes both logs and metrics
  
# Azure Data Explorer
- data exploration service for log and telemetry data
- can handle multiple data streams
- analyze large volumes of diverse data from any data source (websites, apps, IoT devices, and more)
- use ADE for diags, monitoring, reporting, Machine Learning, and other analytics tasks
  
# Backup for Disaster Recovery
- on-prem : files, folders, system state with Microsoft Azure Recovery Services (MARS) agent. use System Center Data Protection (SCDP) or Azure Backup Server (MABS) agent to protect on-prem VMs.
- backup entire Windows or Linux VMs (using backup extensions)
- Azure Files backup to a storage account
- backup SQL server databases running on Azure VMs
- backup SAP HANA databases running on Azure VMs
  
- Azure backup organizes backup data into a vault. A vault stores backup copies, recovery points, and backup policies. Two types of vaults.
  1) Azure Backup Vault - used with Azure Backup only
  2) Azure Recovery Services Vault - can be used by Azure Backup or Azure Site Recovery
- consider Azure Policy to apply consistent policy across all your vaults
- consider using more than one vault, to separate prod & dev, organize by region
- consider using RBAC to secure your vaults
- consider redundancy for your vaults. LRS to protect against failure in a datacenter. ZRS to replicate data across zones in the same region. GRS to protect against region-wide outages.
- consider using Resource Guard to require approval from another user for important backup actions. Add MFA to increase security.
- consider centralized management of all your vaults with Resiliency in Azure.
  
# Azure Blob Backup
- soft delete at container level protects the entire container and all blob contents
- soft delete at blob level protects deletion of individual blobs, snapshots, versions for a retention period
- blob versioning allows you to roll back to previous versions (recall NetApp single item rollback through Windows previous version feature)
- operational backup for blobs provides continuous backup. You don't have to schedule any backups.
- operational backup stores data in the storage account, NOT a vault
  
# Azure Files Backup and Recovery
- share snapshots capture the share state at that specific point in time
- snapshots can be created manually by using Azure portal, REST API, client libraries, CLI, and PowerShell
- snapshots can be automated with Azure Backup and backup policies
- retrieval/restore can be at the individual file level
- snapshots are incremental; only change deltas stored
- you can't delete a share than contains snapshots, you must delete the snapshots first
- two methods for backing up file shares:
  1) vaulted backup stores backup data in a vault, supports retention up to 10 years. This is the recommended appraoch for comprehensive data protection.
  2) snapshot backup creates snapshots that are stored locally within the storage account and are managed via Recovery Services vault metadata. Faster for restores but cannot protect against storage account deletion or ransomware because the snapshots live INSIDE the same storage account.
    - azure backup keeps metadata about the snapshots in the Recovery Services vault, but not the actual data or changes.
    - you can configure snapshots for daily, weekly, monthly, or yearly retention
- consider instant restore - snapshots
- consider alerts and reporting on failures
- Azure backup uses server endpoint Windows Volume Shadow Copy Service (VSS) snapshots. You can configured the ability to self-restore to users (advanced/super users)
  
# Azure Virtual Machine Backup and Recovery
- Azure backup allows for simple configuration scaling for Windows and Linux VMs.
- Azure VM backup offers two policy types:
  1) standard policy - once a day backup with standard snapshot storage. (does not support Trusted Launch VMs, Ultra Disks, Premium SSD v2)
  2) enhanced policy - supports backups as frequently as every 4 hours, ZRS snapshots, newer disk types: Ultra Disks, Premium SSD v2. Supports Trust Launch Vms.
- VM backup process is first a VM snapshot is taken and stored locally, then the snapshot is transferred to Recovery Services vault for longer term storage. In the vault, the backup recovery points are managed through the vault.
- VM backups are encrypted at rest with Storage Service Encryption (SSE)
- consider during VM restores that too much data can be throttled. consider splitting your VM restores out with separate storage accounts, one for each VM restore
- consider Cross Region Restore (CRR) - restore VMs in a secondary region (Azure paired region). CRR works with VMs, SQL databases, and SAP HANA databases.
  
# Azure SQL Backup and Recovery
- automated backups of SQL Database and SQL Managed Instance with SQL backup technology
 1) full backups once a week
 2) differential backups every 12-24 hours
 3) transaction log backups every 5 to 10 minutes
- restore a database to a point in time in the past
- restore a deleted database to time of deletion
- restore a database to another geographic region
- restore a database from a long-term backup
- SQL Database automatic backups are kept for 35 days.
  - for longer retention use the long-term retention (LTR) feature to keep backups in Azure Blob Storage for up to 10 years
  
# Azure Site Recovery
- replicate Azure VMs for failover to secondary region
- replicate on-premises VMs to Azure or a secondary on-premises datacenter
- replicate workloads
- automate BCDR tasks like automated periodic test failovers
- ASR provides continuous replication with frequency as low as 30 seconds for Hyper-V
- use app-consistent snapshots which capture disk data, memory data, and all in-process transactions
- run DR tests without affecting ongoing replication
- groups VMs, add scripts and manual actions, integrate recovery plans with Azure Automation runbooks
  
# High Availability and Disaster Recovery
- Recovery Time Objective (RTO) - maximum time available to bring resources online
- Recovery Point Objective (RPO) - maximum amount of data loss that the business is willing to accept
- IaaS versus PaaS - 
  - IaaS, you are responsible for the OS and the installation of apps and databases; along with that the configurations and HADR solutions.
  - PaaS, the service is managed by Azure along with the HADR solution (built-in)
- Failover Cluster Instance (FCI) - for Azure FCI, an internal load balancer (ILB) is required
  1) FCI requires shared storage; Premium file share, iSCSI, Azure Shared Disk, Storage Spaces Direct (S2D), or 3rd party solution like Sios DataKeeper.
  2) FCI on Standard Edition of SQL Server can have max 2 nodes
  3) FCI on Azure requires AD DS and DNS implemented in Azure.
- Availability Groups (AGs) provides a primary and up to 8 secondary replicas (Enterprise SQL)
  1) each replica maintains a full copy of database
  2) replication can be sync or async
  3) secondary replicas can be configured to offload tasks from the primary. example backups or read-only mode
  4) AGs use a listener for abstraction which functions like the unique name assigned to a FCI.
    
- Log Shipping
  1) database level protection
  2) take a full backup of primary and restore it to a secondary server in loading state (STANDBY or NORECOVERY) - this is known as warm standby or secondary database
  3) primary then backs up transaction logs and copies the backup to the secondary server nad restores it onto the standby
  
- Azure High Availability for IaaS
  1) Availability Sets - logical grouping of resources with anti-affinity rules to provide separation by fault domains (rack failures) and update domains (update groups)
  2) Availability Zones - separate resources across datacenters in same region (zones 1, 2, 3)
  3) Azure Site Recovery - replication to another region to provide failover (RTO 2 hours)
  
- PaaS options for HADR
  1) database availability - Accelerated Database Recovery (ADR) is built in. The transaction log is truncated aggressively and a persisted version store (PVS) is used. This allows instant transaction rollback. ADR is on by default and can not be disabled.
  2) database consistency - regular backup and restore checks are run. multiple copies of your data and backups exist both locally and across regions. CHECKSUM is on by default. Automatic page repair is on. Detection for lost write and stale read is in place.

- IaaS options for HA (SQL running on your VMs)
  1) Always on availability groups (high availability)
    1) no shared storage
    2) works well with patching/updating
    3) apps can access both primary and secondary replicas
  2) Always on Failover Cluster Instance
    1) works well with patching/updating
    2) easy, standardized method for apps to access the clustered instance of SQL server
- IaaS options for DR
  1) Multi-region or Hybrid Always on Availability Group
    1) AG is stretched across datacenters in different regions
    2) requires AD DS and DNS to be running in each region and on-premises (hybrid)
    3) HA and DR protection
  2) distributed availability group
    1) enterprise edition feature of SQL
    2) primary replica is known as the Global Primary it has a secondary replica server in its AG.
    3) the primary replica in the second AG is known as a FORWARDER and keeps the secondary replicas in sync.
    4) there are two AGs and these are bound into another AG. AG of AGs.
    5) separates out the WSFC (Windows cluster) as a single point of failure if all nodes lose communication
    6) one primary isn't syncronizing all replicas, it syncs the Forwarder and offloads the remote replicating there.
    7) provides failback from one location to another.
  3) log shipping
    1) tried and true feature that has been around for over 20 years
    2) easy to deploy and administer
    3) log shipping is tolerant of networks that aren't robust
    4) log shipping meets more RTO and RPO goals for DR
    5) log shipping is a good way to protect FCI because the logs are transmitted to another location for protection.
    6) during failure, still will lose some data as it doesn't finish committing to the log (assumption)
  4) Azure Site Recovery (ASR)
    1) works with any server, VMs, etc
    2) replicates the server to another location
    3) part of Azure platform
  5) Hybrid Solutions
    1) hybrid solutions are IaaS based since they rely on traditional infrastructure.
    2) a big constraint is connecting the network to on-Premise. ExpressRoute is one solution to help with latency/bandwidth.

# Design for Azure SQL Database
- Azure SQL Database is highly scalable
- large databases up to 128 TB or autoscaling for unpredictable workloads (serverless)
- elastic database pool - all databases in the pool share the same pool of resources
- two pricing options:
  1) DTU (Database Transaction Unit): simple, preconfigured, blended measure of CPU, mem, reads, writes
  2) vCore: flexible, you control, transparent, independent scaling of compute, storage, I/O resources
- serverless, available for General Purpose or Hyperscale databases, automatically scales compute and charges for what you use. Hyperscale also supports large storage.
- Azure Hybrid Benefits, a licensing mode that allows you to use your existing on-prem SQL licenses to allocate Azure Databases in the vCore cost plan.
- Azure SQL Database (fully managed instances) has the highest industry uptime.
- free offer for lifestime of subscription: 10 Generate Purpose single databases, each with 100,000 vCore seconds of compute per month. Good for dev
- reserved capacity allows you to pre-pay for a chunk in advance for a lower price
- consider serverless option for single database, scales compute automatically, and only pay as you consume
- elastic pool allows grouped databases to share shifting resource demands within the pooled amount configured.
  
# Design for Azure SQL Managed Instance
- good for lift and shift migrations to Azure without having to redesign apps
- good for customers with instance-scoped features: SQL Server Agent, Common Language Runtime (CLR), Database Mail, Distributed Transactions, Machine Learning Services
- uses vCore mode
- includes almost all features of SQL Server
- Azure managed patching, updates, backups, HA
- use Azure AD and AD Connect to sync on-prem identities to Azure
- single instance or instance pool
- free instance for 12 months after creation - good for evaluation, validate compatibility before migration
- upgrade to Next-gen General Purpose for more capacity: 500 databases for instance, 32 TB of storage, can scale resources independently. same baseline cost for Next Gen as General Purpose. Difference is you can scale different areas, which in turn could cost more with consumption (I/O)
  
# Design for SQL Server on VMs
- access to full capabilities of SQL Server since you control the server on the VM
- you are responsible for version updates, patching for OS and SQL Server
- features like SSAS, SSRS, SSIS
- can leverage Azure backups, security updates, Point-in-time restores, accelerated storage performance with Azure Blob Caching
- leverage Azure Hybrid Benefit licensing
  
# Database Scalability
- vertical scaling - scale compute up or down. elastic database pools allow you to allocate resources for when your pooled databases needs them
- horizontal scaling - add or remove databases by using sharding to partition data or read scale-out provisioning.
- elastic pools:
  1) basic - up to 5 eDTUs per database
  2) standard - up to 100 eDTUs per database
  3) premium - up to 1000 eDTUs per database
- elastic tools and elastic query are capable of performing functions across multiple databases in Azure SQL Database

# Database Availability
- General Purpose Tier - for common workloads, budget oriented balance, backup files replicated (RA-GRS, LRS, ZRS)
- Business Critical / Premium Tier - highest resilience to failures by using several isolated replicas. Backups are replicate (LRS, ZRS, RA-GRS) and logs 
- Hyperscale Tier - designed for very large OLTP databases (100 TB), autoscale storage and compute, snapshot backups, scales up or down in realtime, restores in minutes
- Azure SQL is built on Azure Service Fabric

# Security for data at rest, data in motion, and data in use
- rest = stored. Transparent data encryption (DTE) always encrypted
- motion = in transit. Transport Layer Security (TLS 1.2 or higher) always encrypted
- process = open and being changed. Dynamic data masking. specific data is unencrypted, remaining data is encrypted.
  
# Azure Cosmos DB and Table Storage
- Azure Cosmos DB is fully managed NoSQL database service
- relational data = SQL
- semi-structured data, schema-on-read = CosmosDB SQL
- apps written for Table Storage can migrate to Cosmos DB for Table with few code changes
- CosmosDB has multiple APIs that allow you to use many 3rd party DB formats (MySQL, PostgreSQL, MariaDB, Cassandra, MongoDB) inside CosmosDB. Move the data to Azure CosmosDB and use the API so don't have to change much in your app.
- available globally
- consumption based pricing model
- SLA is 99.99% availability

# Design for Storage
- Blob Storage - unstructured data, often images and multimedia files
- Azure Files - fully managed file shares with SMB, NFS and REST API access
- Azure Managed Disks - acts like physical disks, think disks for VMs
- Azure Queue Storage - store large number of messages, commonly used to create a backlog of work to process async.
  
# Storage Accounts
- groups together all your storage under a unique namespace that is accessible globally via HTTPS. massively scalable, protected, secure, HA
- collection of settings for your storage: location, replication strategy, subscription owner
  1) standard general purpose v2 - blob storage, data lake, queue storage, table storage, azure files, disks (page blobs)
  2) premium block blobs - blob storage, data lake, high transaction rate, smaller objects
  3) premium file shares - file shares (smb, nfs) for enterprise or high-performance scale apps
  4) premium page blobs - high-performance account for page blobs. idea for data disks, OS, databases
  
# Data Redundancy
- redundancy is acheived by replicating data to a primary region
- storage accounts have a primary region
- primary region supports LRS or ZRS
- replication can be done for a secondary region. region-pairs. GRS and GZRS.

# Storage for Blob
- Hot tier = 99.9% availability
- Cool tier - 99.0% availability
- Cold tier - 99.0% availability
- Archive tier - 99% availability
- immutable storage - WORM (Write Once Read Many) state. Data can't be modified or deleted for a user-specific interval.
  1) time-based retention policies
  2) legal hold policies
  
# Azure Files
- direct mount of file shares (serverless)
- cache Azure file shares on-premises with Azure File Sync
- four tiers of storage
  1) premium - SSD drives, high performance, low-latency
  2) transaction optimized (standard storage hardware)
  3) hot access tier (standard storage hardware)
  4) cool access tier - cost-efficient storage optimized for online arhive storage scenarios.
  
# Azure Managed Disks
- several types of managed disks
  1) Ultra-disk (SSD IO intensive) *not avail in all regions
  2) Premium SSD v2 (SSD Prod Performance, high IOPS, low latency) *not avail in all regions
  3) Premium SSD (SSD Prod Perf)
  4) Standard SSD (SSD Web servers, dev/test)
  5) Standard HDD (backup, non-critical, infrequent access) *retiring on September 8, 2028
- several types of encryption for managed disks
  1) Azure Disk Encryption (ADE) - encrypts VMs so only the VM that owns the disk can access it
  2) Server-Side Encryption (SSE) - physical disks in the datacenter are encrypted (encryption at rest)
  3) Encryption at Host - the server hosting your VM provides the encryption.
 
#  Storage Security
- SAS - shared access signatures (access tokens)
- firewall policies and rules
- secure transfer rejects any request originating from nonsecure connections *default on
- data is automatically encrypted: two ways to manage encryption keys at the storage account level:
  1) Microsoft-managed keys
  2) Customer-managed keys (CMK) - stored in key vault
  
# Data Integration with Azure Data Factory
- cloud based ETL and data integration service that can help you create and schedule data-driven workflows (called pipelines) that can ingest data from disparate data stores.
- four major steps to create the workflow (pipeline)
  1) connect and collect - ingest the data from different sources into a centralized location
  2) transform and enrich - transform by using a compute service like Azure Databricks and Azure HDInsight Hadoop
  3) provide continuous integration and delivery (CI/CD) and publish - support CI/CD by using GitHub and Azure Pipelines to deliver the ETL process incrementally before publishing the data to the analytics engine
  4) monitor - monitor the pipeline for scheduled activities and for any failures
- linked services define the required connection information needed for ADF to connect to external resources
- ADF publishes the final dataset which can then be consumed by technologies like Power BI or Machine Learning
- ADF supports 100+ connectors
  
# Data Integration with Data Lake
- a data lake is a repository of data stored in its natural format, usually as blobs of files.
- Azure Data Lake uses the same redundancy options as Azure Blob Storage
- Azure Data Lake is priced at Azure Blob Storage levels
- support RBAC and ACL
- realtime data ingestion from Apache Storm, Azure HDInsight, Azure IoT Hub, Azure Event Hubs, or Azure Stream Analytics.
- good for large volumes of text data
- must manually configure data replication (unlike blob storage)
- supports hierarchical namespaces
- Hadoop compatible
- granular access security
  
# Data Integration with Azure Databricks
- fully managed Big Data and Machine Learning platform
- takes data from data lake and creates a data brick
- Azure Databrick is based on Apache Spark
- three environments for developing data intensive applications
  1) Databricks SQL - run SQL queries on your data lake
  2) Databricks Data Science & Engineering - lets data teams work together in an interactive workspace. Data is brought into Azure through batch or real-time tools like ADF, Kafka, Event Hubs, or IoT Hub.
  3) Databricks Machine Learning - end-to-end machine learning environment
  
# Data Integration with Azure Synapse Analytics
- full set of tools for data analysis: data ingestion, exploration, transformation, and management, and supports analysis for all your BI and machine learning needs
- four different areas of analytics:
  1) Descriptive analytics - what is happening
  2) Diagnostic analytics - why is it happening
  3) Predictive analysis - what is likely to happen
  4) Prescriptive analysis - what needs to be done
- implements massively parallel processing (MPP) architecture
- control node and a pool of compute nodes
- submit queries in the form of Transact-SQL statements
- uses Polybase
- Azure Synapse Analytics is composed of five elements:
  1) Synapse SQL pool
  2) Synapse Spark pool
  3) Synapse Pipelines
  4) Synapse Link
  5) Synapse Studio
- does not support cross reion data flows
- monitor Spark jobs for data flow by using Synapse Spark pools
  
# Hot, warm, cold data paths
- warm data path - data stream processed near real time as it flows through the system
- cold data path - consists of a batch layer and serving layers that provide a long-term view of the system.
- hot data path - processing or displaying in real time. real-time alerting and streaming operations. latency-sensitive data results need to be ready in seconds or less.
  
# Azure Stream Analytics
- fully managed PaaS, real-time analytics and complex event-processing engine
- examples: IoT device dta, sensors, clickstream, and social media feeds
- works on the following concepts:
  1) data streams - continuous data generated by apps, IoT devices, or sensors.
  2) event processing - consumption and analysis of a continuous data stream to extract actionable insights from the events happening within that stream.
- Azure Stream Analytics supports processing events in three data formats:
  1) CSV
  2) JSON
  3) Avro
- stream analytics ingests data from Azure Event Hubs, Azure IoT Hub, or Azure Blob Storage.
- low cost. billing is done by Streaming Units (SUs) consumed
- run in the cloud for large-scale analytics. For ultra-low latency analytics, run Stream Analytics on IoT Edge or Azure Stack.
- secure. all inbound and outbound communications are encrypted and supports TLS 1.2.
- doesn't store data, just analyzes the stream in-memory
- no code, no install, drag and drop apprach that complements the SQL query language
  
# Choose Compute Service
- serverless means no server to manage, Azure manages it and you just worry about the services it provides. usually also means that you don't RDP or SSH into a server to manage the services although there might be a mini-shell
- VMs/IaaS is full control of OS and VM resources. you manage, patch, update
- Azure Batch - large-scale parallel and high-performance computing (HPC) applications. *keywords: batch, parallel, jobs, large # of tasks
- Azure App Service - host web apps, mobile app backends, RESTful APIs
- Azure Functions - run code in the cloud. complex code is okay
- Azure Logic Apps - platform to create and run automated workflows similar to capabilities in Azure Functions. low code / no code. orchestrate workflows
- Azure Container Instances (ACI) - run containers, without creating VMs
- Azure Container Apps (ACA) - run containerized applications, fully managed, serverless platform. supports scale to zero, Dapr integration, jobs, revision-based traffic management.
- Azure Kubernetes Service (AKS) - run containerized applications with managed Kubernetes service. large scale orchestration.
  
# Virtual Machines
  1) General Purpose
  2) Compute optimized
  3) Memory optimized
  4) Storage optimized
  5) GPU
  6) HPC
  
# Azure Batch
- works well with apps that run independently (parallel workloads)
- HPC jobs
- can scale to thousands of VMs
- you configure and define how many VMs in the pool
- service runs the jobs, requeues work, identifies failures, and scales down the pool when completed
  
# Azure App Service
- HTTP based service, ideal for web hosted apps, background jobs, mobile backends, RESTful APIs
- automatic scaling and HA
- PaaS environment
- supports development in multiple languages and frameworks
- built-in load balancing and traffic maangement at global scale with HA
- deployment slots make continuous deployment easy
- web apps, API apps, WebJobs
  
# Azure Container Instances (ACI)
- simple apps, task automation, build jobs
- fast startup, persistant storage, per second billing
- Azure file shares can be mounted directly to a container to retrieve and persist state
- Linux and Windows
- container groups contain a collection of containers that get scheduled on the same host machine.
- consider using a private registry (security)
  
# Azure Kubernetes Service (AKS)
- Kubernetes is an open-source platform for automating deployment, scaling, and management of containerized workloads
- container management and orchestration at scale
- automatically update running instances
- AKS has three cluster managment pricing tiers:
  1) free - no SLA guarantee (good for dev/test)
  2) standard - hourly control plane charge with uptime SLA (good for prod)
  3) premium - 24-month long term support
- clusters created with ARM templates or Bicep files.
- by default supports Docker file image format
  
# Azure Functions
- code-first technology
- event driven code
- compute on demand
- automatic scaling up and down
  
# Azure Logic Apps
- create and run automated workflows
- design-first technology
- create orchestration with a GUI or by editing config files
- integrate legacy and modern systems across cloud, on-premises, and hybrid environments
- 100's of external connectors
- scales automatically
  1) consumption plan - multitenant, pay-per-execution
  2) standard plan - single tenant, dedicated compute resources
  


