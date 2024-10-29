---
tags: 
netgroups: 
lead-engineer: 
manager(s): 
code_name: 
products:
---

## Links


## Documentation

NetApp ONTAP Cloud Manager (often referred to as NetApp Cloud Manager or OCCM) is a centralized management solution provided by NetApp for managing, monitoring, and orchestrating NetApp's cloud storage systems. It provides a unified interface to manage both on-premises and cloud-based storage environments, facilitating hybrid cloud architectures.

Here are some key features and functionalities of NetApp Cloud Manager (OCCM):

1. **Centralized Management**: Allows for the management of multiple NetApp ONTAP instances across different environments (on-premises, private cloud, and public cloud).

2. **Automation and Orchestration**: Automates the deployment and configuration of ONTAP instances, simplifying the process of setting up and maintaining storage infrastructure.

3. **Data Protection and Security**: Provides tools for data protection, including backup, disaster recovery, and data encryption, ensuring that data is secure and recoverable.

4. **Monitoring and Reporting**: Offers comprehensive monitoring and reporting capabilities to track the performance, capacity, and health of storage systems.

5. **Cost Management**: Helps in managing and optimizing storage costs by providing insights into storage usage and facilitating cost-effective storage solutions.

6. **Integration with Cloud Providers**: Integrates with major cloud providers like AWS, Azure, and Google Cloud, enabling seamless management of cloud storage resources.

7. **Data Mobility**: Facilitates data mobility and replication between different environments, supporting hybrid and multi-cloud strategies.

8. **User-Friendly Interface**: Provides a user-friendly graphical interface and RESTful APIs for easy management and integration with other tools and systems.

NetApp Cloud Manager is particularly useful for organizations looking to leverage hybrid cloud storage solutions, providing a comprehensive toolset to manage and optimize their storage infrastructure across diverse environments.


## Engineers (modify the query below)


```dataview
TABLE office, grade, manager, organization, title
FROM ("300 NetApp/People")
WHERE contains(products, "OCCM") or (typeof(products) = "array" AND contains(products, [[NetApp-Product - ONTAP Cloud Manager - OCCM]]))
sort office

```


## Notes
