![iat-insurance-group-logo](https://user-images.githubusercontent.com/10728023/109661929-7ec29b00-7b38-11eb-927a-601d19eb0026.jpg)
# Azure Foundation

## Objectives
1.	Create a consistent set of expectations and processes for Azure migrations.
1. Establish a standardized decision making framework that enables stakeholders to consistently evaluate:
    * Whether to migrate existing applications to Azure or to leave applications on existing infrastructure.
    * The underlying data that supports that decision (price, time, availability, etc). 

## Migration Process

![migration-phases](https://user-images.githubusercontent.com/10728023/110350114-669fbf80-8001-11eb-80ef-a0b8f19546f0.png)

### One-Time Initialization ("Upfront Actions")
* Azure Tenant (John)
    * Organization in Azure AD
* Landing Zone
    * A set of well defined resources, environments, and policies that enforce consistency
    * Includes:
        <details>
            <summary>Management Group Hierarchy</summary>

        * Used to organize and manage subscriptions. ([reference](https://docs.microsoft.com/en-us/azure/governance/management-groups/overview))
        * Subscriptions inherit conditions from management groups (i.e. forces consistency)
        * Establishes user permissions (RBAC) in a central location.
        </details>

        <details>
            <summary>Policies</summary>

        * Enforce VM monitoring (Windows & Linux)
        * Enforce VMSS monitoring (Windows & Linux)
        * Enforce Azure Arc VM monitoring (Windows & Linux)
        * Enforce VM backup (Windows & Linux)
        * Enforce secure access (HTTPS) to storage accounts
        * Enforce auditing for Azure SQL
        * Enforce encryption for Azure SQL
        * Prevent IP forwarding
        * Prevent inbound RDP from internet
        * Ensure subnets are associated with NSG
        </details>

        <details>
            <summary>Subscriptions</summary>

        * Management - Security monitoring, logging, diagnostics
        * Connectivity - Hub vNet, Firewall, VPN gateway
        * Identity - Active Directory controllers
        * Corporate Connected Workloads - That communicate with on-prem infrastructure
        * Azure Native Applications - For internet facing applications.
        </details>

        <details>
            <summary>Resource Groups</summary>

        * Containers for resources that share common functions within a subscription.
        * Facilitates streamlined cost analysis.
        
        ![image](https://user-images.githubusercontent.com/10728023/109846973-b86cd200-7c1c-11eb-9cdc-9317b7962127.png)
        </details>
    ![image](https://github.com/Azure/Enterprise-Scale/raw/main/docs/reference/adventureworks/media/es-hubspoke.png)

* Pricing - Upfront costs are minimal. __$10s-$100s / month__
* Limited Effort - Infrastructure Templates
* Hybrid Networking
    * Options
        <details>
            <summary>VPN Gateway</summary>

        * ~10 Gbps ([throughput](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpngateways))
        * Site-to-Site (S2S) -> [Supported Devices](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-devices)
        * Point-to-Site (P2S) -> [Supported Protocols](https://docs.microsoft.com/en-us/azure/vpn-gateway/point-to-site-about)
        * Hub & Spoke

        ![image](https://user-images.githubusercontent.com/10728023/109803620-46ca5f00-7bef-11eb-97d6-3265ff5a31f3.png)
        </details>

        <details>
            <summary>ExpressRoute</summary>

        * Private connections (WAN) between Azure datacenters and infrastructure on your premises or in a colocation environment.
        * Up to 100 Gbps
        * Locations: Atlanta, Chicago, Dallas, Denver, Las Vegas, Los Angeles, Los Angeles2, Miami, Minneapolis, Montreal, New York, Phoenix, Quebec City, Queretaro(Mexico), Quincy, San Antonio, Seattle, Silicon Valley, Silicon Valley2, Toronto, Toronto2, Vancouver, Washington DC, Washington DC2
        * [Providers](https://docs.microsoft.com/en-us/azure/expressroute/expressroute-locations-providers)
        * [Reference](https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/expressroute)

        ![image](https://user-images.githubusercontent.com/10728023/109800767-99a21780-7beb-11eb-8a7c-7c9897ecbe48.png)
        </details> 

        <details>
            <summary>Virtual WAN</summary>

        * For > 30 S2S connections
        * ~100 Gbps
        * All traffic is routed through the hub.
        * Gateways are managed and scaled for you. ([reference](https://docs.microsoft.com/en-us/azure/virtual-wan/virtual-wan-about))

        ![image](https://user-images.githubusercontent.com/10728023/109809005-cce9a400-7bf5-11eb-87be-c5a1f0758b28.png)
        </details>
    * Must identify current private IP address ranges for existing infrastructure.

### Incremental Migration 
* Azure Migrate - Provides a centralized migration tool for planning, assessing, and migrating.
* Process
![migration-process](https://user-images.githubusercontent.com/10728023/109860272-ec032880-7c2b-11eb-9d05-a070a93dc6b2.png)
* Architecture 
![migration-architecture](https://user-images.githubusercontent.com/10728023/109860362-0ccb7e00-7c2c-11eb-8152-5b2c0bcfe072.png)
* Supported Servers
    * Hyper-V
    * VMWare
    * Physical
* Supported Databases
    * SQL Server 2005-2017
* Supported Web Applications
    * .NET
    * .PHP
* Data Migration
    * Azure Data Box - physical or virtual transfer ([reference](https://azure.microsoft.com/en-us/services/databox/))
* Performance Based Assessments

<img width="425" alt="assessment-summary" src="https://user-images.githubusercontent.com/10728023/110353579-39eda700-8005-11eb-8044-0ff4cf5eb53f.png">

#### Considerations
* DNS
    - Azure DNS
    - On-prem DNS
    - Hybrid DNS

    ![image](https://user-images.githubusercontent.com/10728023/109872461-72266b80-7c3a-11eb-8639-2b90e748a553.png)

#### Forward Looking
* Automation
    * Deployments
    * Alerts & Notifications
    * DevOps
* Disaster Recovery Plan
    * Recovery Point Objective (RPO)
    * Recovery Time Objective (RTO)
* Decompose/Refactor Applications
    * Azure App Service
    * Containers & Orchestration (Kubernetes)
    * Azure Functions

![build-measure-learn](https://user-images.githubusercontent.com/10728023/110351178-8edbee00-8002-11eb-8857-e0a1fba82c95.png)

## Decision Making Framework
* <details>
    <summary>Decision Process</summary>


    ![IAT Azure Migration - Decision Flow Chart](https://user-images.githubusercontent.com/10728023/110042039-24316680-7d13-11eb-8b27-8883060c6752.png)
</details>

* Soft Pricing - [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/)
* Hard Pricing - [Azure Migrate Service](https://azure.microsoft.com/en-us/services/azure-migrate/)
* <details>
    <summary>Cloud Models</summary>


    ![Microsoft-Azure-Cloud-Models](https://user-images.githubusercontent.com/10728023/110042616-0a445380-7d14-11eb-984b-cfa5e64b5010.png)
</details>

* The first resources that should be migrated should be the lowest risk (i.e. less traffic, internal use, etc)

## Final Thoughts
* Azure Centric - 3rd party tools are becoming less
* Long Term Goals
    - Hands Off -> Manged Services
    - Greater Control -> Automation & DevOps