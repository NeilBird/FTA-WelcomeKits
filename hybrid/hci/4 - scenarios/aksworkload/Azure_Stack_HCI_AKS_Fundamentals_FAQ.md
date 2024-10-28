# Welcome Kit – Azure Stack HCI – AKS

> Should contain:
> - a comparison between AKS (Azure) vs AKS hybrid (e.g. HCI) 
> - management, monitoring, networking, storage, HA (DR e.g. replication, backup)
> - operations tasks (e.g. updating)
> does not have to be 100% self written i.e. pointers to already existing docs are fine.  

Welcome to the "Azure Stack HCI – AKS Fundamentals FAQ Welcome Kit." This comprehensive guide is designed to provide you with essential insights into the foundational aspects of Kubernetes, Azure Kubernetes Service (AKS), Resource Bridge, Azure Arc, and the unique integration of AKS with Azure Stack HCI. 

## Fundamentals (Kubernetes, AKS, Azure Stack HCI AKS)
### What are the differences between Kubernetes and AKS?
- Kubernetes is an open-source container orchestration platform that can be run on any infrastructure, while AKS (Azure Kubernetes Service) is a fully managed Kubernetes service provided by Microsoft that runs in the Azure cloud.
- Kubernetes requires manual setup and configuration, while AKS automates much of the setup and management of Kubernetes clusters.
- AKS provides integrated support for Azure services such as Azure Active Directory, Azure Monitor, and Azure Policy, while Kubernetes requires additional configuration to integrate with these services.
- AKS provides built-in security features such as network isolation, role-based access control, and private container registry, while Kubernetes requires additional configuration to implement these features.
- AKS provides automatic scaling of the Kubernetes cluster based on workload demands, while Kubernetes requires manual scaling.
- AKS provides a simplified billing model compared to running Kubernetes on your own infrastructure, as you only pay for the resources used by the AKS cluster.

### What are the differences between AKS and Azure Stack HCI AKS?
- AKS is a fully managed Kubernetes service provided by Microsoft that runs in the Azure cloud, while Azure Stack HCI AKS is a Kubernetes service that runs on-premises on Azure Stack HCI.
- AKS provides integrated support for Azure services such as Azure Active Directory, Azure Monitor, and Azure Policy, while Azure Stack HCI AKS is designed to work with Azure Arc, which provides a unified management experience across on-premises, multi-cloud, and edge environments.
- AKS provides built-in security features such as network isolation, role-based access control, and private container registry, while Azure Stack HCI AKS requires additional configuration to implement these features.
- AKS provides a simplified billing model compared to running Kubernetes on your own infrastructure, as you only pay for the resources used by the AKS cluster. Azure Stack HCI AKS is included as part of the Azure Stack HCI subscription, which has a different billing model.[AKS on HCI pricing](https://azure.microsoft.com/en-us/pricing/details/azure-stack/aks-hci/)

### What are capabilities that Azure Stack HCI aks does not provide compared with AKS itself?
- Azure Stack HCI AKS does not provide the same level of integration with Azure services as AKS, such as Azure Active Directory, Azure Monitor, and Azure Policy.
- **Active Directory**  -  For Azure Stack HCI AKS you will need to create nn Azure AD application and service principal, configuring the AKS cluster to use Azure AD for authentication, and granting the necessary permissions to the service principal.
- **Azure Monitor** - To use Azure Monitor with Azure Stack HCI, you can install the Azure Monitor agent on the HCI hosts and configure it to send data to Azure Monitor.
- **Azure Policy** - Azure Policy can be used to manage policies for Azure Stack HCI and AKS resources. For Azure Stack HCI, you can use Azure Policy to manage policies for virtual machines, storage accounts, and other resources that are part of your HCI cluster. For AKS, you can use Azure Policy to manage policies for Kubernetes resources, such as pods, services, and deployments. You can create custom policies or use built-in policies provided by Microsoft to enforce compliance with your organization's standards and best practices.

- Azure Stack HCI AKS may not have the same level of scalability as AKS, as it may be limited by the resources available on the on-premises infrastructure.
- **Adding/Removing Nodes** - Add or remove nodes from your HCI cluster using the Azure Stack HCI management tools or PowerShell cmdlets. When adding nodes, ensure that they meet the hardware and software requirements for your HCI cluster. Once the nodes are added or removed, configure the HCI cluster to use the new resources. You can do this using the HCI management tools or PowerShell cmdlets.
- **Scale out your HCI resources in case of a disaster or outage** - use Azure Site Recovery. Azure Site Recovery provides disaster recovery and business continuity solutions for your HCI cluster by replicating your HCI resources to another location.
- **Set up Recovery Services Vault and Configure Replication** - Begin by creating a Recovery Services Vault in Microsoft Azure, and then configure it to enable the replication of your Hyper-Converged Infrastructure (HCI) resources to Azure. This establishes the foundation for the disaster recovery solution.
- **Install Azure Site Recovery Provider and Configuration** - Install the Azure Site Recovery Provider on the nodes of your HCI cluster. This provider facilitates the replication process. Configure these nodes to replicate the designated resources (such as virtual machines, applications, and data) to the previously set up Recovery Services Vault in Azure.
    - [Set up the configuration server for disaster recovery of physical servers to Azure using Azure Site Recovery](https://learn.microsoft.com/en-us/azure/site-recovery/physical-azure-set-up-source): This article describes how to set up your on-premises environment to start replicating physical servers running Windows or Linux into Azure. It includes information about prerequisites, hardware requirements, software requirements, and network requirements.
  - [Set up disaster recovery of physical on-premises servers with Azure Site Recovery](https://learn.microsoft.com/en-us/azure/site-recovery/physical-azure-disaster-recovery): This tutorial shows how to set up disaster recovery of on-premises physical Windows and Linux servers to Azure. It includes information about creating a Recovery Services vault for Site Recovery, creating a replication policy, and enabling replication for a server.
  - [Manage the configuration server for physical servers in Azure Site Recovery](https://learn.microsoft.com/en-us/azure/site-recovery/physical-manage-configuration-server): This article provides information about managing the configuration server for physical servers in Azure Site Recovery. It includes information about running the Unified Setup installation file, selecting the Install the configuration server and process server option, and specifying how the Provider running on the configuration server connects to Azure Site Recovery over the Internet.
  - **Test Disaster Recovery Solution** - Perform a controlled failover test to evaluate the effectiveness of your disaster recovery solution. This entails initiating a failover process that switches your HCI resources from the on-premises environment to the replicated resources within the Recovery Services Vault in Azure. This step ensures that the disaster recovery setup is functional and can be relied upon during actual outages.
  - **Monitor Replication Status and Health** - Continuously monitor the replication status and overall health of your HCI resources. Regularly check that the replication process is up-to-date and accurate in the Recovery Services Vault. This monitoring ensures that your HCI resources remain prepared for failover in the event of an unplanned outage or disaster scenario.

- Azure Stack HCI AKS may not have the same level of automation and ease of use as AKS, as it may require more manual configuration and management.
    - **Deployment** - Deploying Azure Stack HCI AKS may require more manual configuration compared to AKS, as it involves setting up the Azure Stack HCI infrastructure and configuring the AKS service on top of it.
    - **Scaling** - Scaling Azure Stack HCI AKS may require more manual configuration compared to AKS, as it may involve adding or removing nodes from the on-premises infrastructure and configuring the AKS service accordingly.
    - **Upgrades** - Upgrading Azure Stack HCI AKS may require more manual configuration compared to AKS, as it may involve upgrading the Azure Stack HCI infrastructure and then upgrading the AKS service on top of it.*
    - **Monitoring** - Monitoring Azure Stack HCI AKS may require more manual configuration compared to AKS, as it may involve setting up monitoring tools on the on-premises infrastructure and configuring them to work with the AKS service.
- Azure Stack HCI AKS may not have the same level of security features as AKS, as it may require additional configuration to implement features such as network isolation, role-based access control, and private container registry.
    - **Network isolation** - Additional configuration may be required to implement security features such as network isolation.
    - **RBAC** - Additional configuration may be required to implement role-based access control (RBAC).
    - **Azure AD authentication and authorization** - RBAC may require configuring Azure AD authentication and authorization, and defining RBAC policies.
    - **Private container registry** - Additional configuration may be required to implement a private container registry.
    - **Setting up a private registry** - Private container registry may require setting up a private registry in Azure Container Registry or another container registry service.
    - **Configuring AKS** - Private container registry may require configuring AKS to use this registry.
    - **Security considerations** - It is important to carefully consider the security requirements of your AKS workloads and ensure that appropriate security measures are in place to protect your resources.
- Azure Stack HCI AKS may not have the same level of billing simplicity as AKS, as it is included as part of the Azure Stack HCI subscription, which has a different billing model.

### Can you explain the relationship between Azure Stack HCI AKS, Resource Bridge, and Azure Arc?
- **Azure Stack HCI AKS** - is a hybrid cloud solution that allows you to run Kubernetes workloads on-premises using Azure Stack HCI. 
- **Resource Bridge** - an Azure Stack HCI feature, offers seamless management of on-premises resources through Azure tools, including HCI resources, Windows Server, Hyper-V, and Storage Spaces Direct. This enables utilization of Azure management tools like Azure Monitor, Azure Security Center, and Azure Update Management for consistent monitoring and management of on-premises assets, ensuring a unified experience across diverse environments. Moreover, Resource Bridge facilitates deployment and management of virtual machines on your HCI cluster using familiar Azure tools, streamlining the oversight and control of your hybrid cloud setup.  To deploy and manage virtual machines on your HCI cluster using familiar Azure tools, you can use Azure Site Recovery, Azure Backup, and Azure Update Management. Additionally, you can use the Azure Portal or Azure PowerShell to manage your virtual machines and perform tasks such as creating and deleting virtual machines, configuring networking, and managing storage.
- **Azure Arc** - is a hybrid cloud management solution that allows you to manage and deploy resources across on-premises, multi-cloud, and edge environments using Azure management tools.

### Is it possible to use the Azure Portal to manage an Azure Stack HCI AKS cluster that is connected to Azure using Resource Bridge?
- Yes, you can use the Azure Portal to manage an Azure Stack HCI AKS cluster with Resource Bridge. Resource Bridge allows you to connect your on-premises Azure Stack HCI cluster to Azure, which enables you to use Azure services such as AKS to manage your on-premises resources. Once you have set up Resource Bridge, you can use the Azure Portal to manage your AKS cluster and perform tasks such as creating and scaling node pools, deploying applications, and monitoring cluster health. However, it's important to note that not all AKS features may be available when using Resource Bridge, so you should consult the official documentation to ensure that the features you require are supported.
### Can I use the same tools and APIs to manage both Azure Stack HCI AKS and AKS?
- No, Azure Stack HCI AKS and AKS are different services and therefore require different tools and APIs for management. Azure Stack HCI AKS is a Kubernetes service that runs on-premises, while AKS is a managed Kubernetes service in Azure. You can use Azure CLI, Azure PowerShell, and the Kubernetes command-line interface (kubectl) to manage AKS, while for Azure Stack HCI AKS, you can use the Azure Stack HCI PowerShell module and the Kubernetes command-line interface (kubectl).
### What are the networking requirements for Azure Stack HCI AKS compared to AKS?
- The networking requirements for Azure Stack HCI AKS and AKS are different due to their different deployment models. 
- For AKS, the Kubernetes cluster is deployed in Azure and uses Azure Virtual Network (VNet) for networking. AKS requires a VNet with at least one subnet to be created before deploying the cluster. 
- For Azure Stack HCI AKS, the Kubernetes cluster is deployed on-premises and uses the physical network infrastructure for networking. Azure Stack HCI AKS requires a dedicated network segment for the Kubernetes cluster, with a minimum of one subnet that can be used for the Kubernetes pods. 
- In both cases, the networking requirements include ensuring that the Kubernetes nodes can communicate with each other and with external resources, such as the internet or other services. Additionally, network security considerations such as firewalls and network segmentation should be taken into account.

### How does Resource Bridge affect the management and deployment of AKS clusters on Azure Stack HCI?
- **AKS on Azure Stack HCI** - If you're running AKS clusters on Azure Stack HCI, Resource Bridge allows you to establish a connection between your on-premises AKS clusters and Azure services. This enables you to manage, monitor, and integrate your on-premises AKS clusters with Azure tools, such as Azure Monitor and Azure Container Registry. For instance, you can use Azure Monitor to gather insights and metrics from your AKS clusters, even though they are deployed on your local infrastructure.
- **Hybrid Scenarios** - In hybrid scenarios, where you have both cloud-based AKS clusters and AKS clusters on Azure Stack HCI, Resource Bridge can help create a consistent management experience. It allows you to use Azure tools to manage both types of clusters, ensuring a unified approach to managing your Kubernetes resources regardless of their location.
### What are Resource Bridge permissions?
- Resource Bridge permissions refer to the authorization settings necessary to connect and manage on-premises resources using Azure Arc. It involves configuring Role-Based Access Control (RBAC) to grant appropriate permissions for Resource Bridge to interact with Azure Arc and other Azure services.
### How does Resource Bridge relate to AKS (Azure Kubernetes Service)?
- Resource Bridge can be used with both AKS (Azure Kubernetes Service) and Azure Stack HCI AKS. For AKS, Resource Bridge can be deployed on an existing AKS cluster or set up as part of the Resource Bridge installation process. This allows you to extend your on-premises environment to Azure and use Azure services to manage and monitor your AKS clusters.
### What are the steps to set up Resource Bridge on an AKS cluster?
- **Create AKS Cluster** - Begin by creating a Kubernetes cluster in Azure using Azure Kubernetes Service (AKS).
- **Install Resource Bridge Helm Chart** - Install the Resource Bridge Helm chart on the AKS cluster. You can find the Helm chart on the Azure Arc GitHub repository.
- **Configure Connection to Azure Arc** - Configure the Resource Bridge to connect to Azure Arc. This entails registering the Kubernetes cluster with Azure Arc and configuring the necessary RBAC permissions to allow Resource Bridge to interact with Azure services.
- **Deploy VM using Resource Bridge** - To deploy a virtual machine (VM) using Resource Bridge, choose the "Guest Configuration" option while creating the VM. This process sets up Azure Arc on the VM, assigning it a Managed Identity for efficient management in Azure.
### What's the benefit of deploying AKS with Resource Bridge?
- **Manage On-Premise Resources** - One of the main benefits is that it allows you to manage on-premises resources using Azure tools and services. This means that you can use familiar Azure tools, such as Azure Monitor and Azure Container Registry, to manage and monitor your AKS clusters, even if they are hosted locally.
- **Unified Management Experience** - By connecting AKS clusters to Azure Arc, you can control them through Azure services, regardless of their location. This means that you can use the same tools and processes to manage AKS clusters in the cloud and on-premises, which can help to simplify management and reduce complexity.
- **Improve security and compliance** - By using Azure services for management and monitoring, you can take advantage of Azure's built-in security features, such as Azure Security Center, to help protect your AKS clusters from threats and ensure compliance with regulatory requirements.
### What is the difference between Resource Bridge and Azure Arc in the context of managing resources that are deployed on-premises?
- **Resource Bridge** - is a feature in Azure Stack HCI that allows you to extend your on-premises environment to Azure. It provides connectivity between on-premises resources and Azure services, allowing you to use Azure tools and services to manage and monitor your on-premises resources.
- **Azure Arc** - is a service that allows you to manage resources across multiple environments, including on-premises, multi-cloud, and edge. It provides a unified management experience for resources that are deployed across multiple environments, using Azure services and tools.
- **Arc more comprehensive** - While both Resource Bridge and Azure Arc can be used to manage resources that are deployed on-premises, Azure Arc provides a more comprehensive solution for managing resources across multiple environments. It allows you to manage resources using Azure services and tools, regardless of their location, which can help to simplify management and reduce complexity.
- **In the context of AKS** - Resource Bridge can be used to provide connectivity between on-premises AKS clusters and Azure services, while Azure Arc can be used to manage and monitor AKS clusters that are deployed on-premises and connected to Azure through Resource Bridge. Together, Resource Bridge and Azure Arc provide a comprehensive solution for managing AKS clusters that are deployed across multiple environments.
### What are the methods and interfaces available for managing resources in both Resource Bridge and Azure Arc, and how do they differ?
- **Resource Bridge** - Managed through the Azure Stack HCI Management tool. Provides a web-based UI for managing on-premises resources. Allows management of virtual machines, storage, networking, and Resource Bridge itself.
- **Azure Arc** - Managed through the Azure portal. Offers a web-based UI for managing resources across various environments. Supports management of virtual machines, Kubernetes clusters, Azure services, and Azure Arc itself. 
- **Automation and Scripting** - Both platforms can also be managed using APIs and command-line interfaces (CLIs). Useful for automation and scripting purposes.
### Can Resource Bridge manage other types of resources besides VMs?
- Yes, Resource Bridge can manage various types of resources beyond VMs. It can be used to connect and manage Kubernetes clusters, databases, virtual machines, and more, regardless of whether they are hosted on-premises or in the cloud.
### How can I deploy AKS cluster(Workload Cluster) on HCI ?
- There are differernt options that you can use to deploy workload clusters. You can use Azure CLI, Azure Portal, Bicep or ARM Templates as well. Windows Administrator Center is not a valid deployment option as of now. You can find more information here [Creating AKS clusters](https://learn.microsoft.com/en-us/azure/aks/hybrid/aks-create-clusters-cli)
### What is az aksarc command for ? 
- With Azure Stack HCI 23H2 version, we introduced a new extension. You can use aksarc extension for your AKS on HCI operations. You can find more information here [az aksarc](https://learn.microsoft.com/en-us/cli/azure/aksarc?view=azure-cli-latest)
### Is Azure Backup supported on AKS on HCI ?
- No, as of now it is not supported. You can leverege 3rd party solutions like Velero. [Velero](https://velero.io/docs/main/) is an open source backup solution for Kubernetes clusters. You can find more information here : https://learn.microsoft.com/en-us/azure/aks/hybrid/backup-workload-cluster
### Does AKS on HCI support Autoscaling? 
- Yes, You can now enable the autoscaling feature when you create or update Kubernetes clusters and node pools.
### Can I use RBAC with AKS on HCI ? 
- Yes, you can now enable Azure RBAC for Kubernetes while creating AKS Arc clusters using Azure CLI and Azure Resource Manager templates.
### Can I use Taint and Labels ? 
- Yes, you can use and update taint and labels.
### Should I update my Azure Stack HCI and AKS on HCI clusters seperately ?
Azure Stack HCI 23H2 consolidates all the relevant updates for the OS, software agents, Azure Arc infrastructure, and OEM drivers and firmware into a unified monthly update package. This comprehensive update package is identified and applied from the cloud through the Azure Update Manager tool.

AKS is now part of Azure Stack HCI starting from version 23H2. The lifecycle management of AKS enabled by Azure Arc infrastructure follows the same approach as any other components on Azure Stack HCI 23H2. More information can be found here : [Cloud-based updates for infrastructure components](https://learn.microsoft.com/en-us/azure/aks/hybrid/cluster-architecture#cloud-based-updates-for-infrastructure-components)
[Updates for Azure Stack HCI, version 23H2](https://learn.microsoft.com/en-us/azure-stack/hci/update/about-updates-23h2)

This does not cover the customer workload clusters, so you need to update your AKS version. You can find the steps here : [Upgrade an Azure Kubernetes Service (AKS) cluster](https://learn.microsoft.com/en-us/azure/aks/hybrid/cluster-upgrade)