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
