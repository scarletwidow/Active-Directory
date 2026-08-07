# Active-Directory
A simulated build of Windows Servers using Azure to demonstrate Active Directory, domain deployment, DHCP/DNS, and Group Policy knowledge.

The desired outcome of this lab is to create a Windows Server virtual machine in Azure, promote the server to a domain controller, build a basic Active Directory structure, create users and groups, and test authentication using both the GUI and PowerShell.

This is shown by creating a domain for an imaginary company, Corp Lab, that has branches in New York, Chicago, and Seattle. For each of these branches, 2-3 users were generated and added. Groups were created for the Corp Lab domain and users were assigned to each group based on their role. 

[Lab Instrustions](https://jakestechlabs.com/labs/ad-basics)

***

# Environment
| Component | Details |
| --------- | ------- |
|    VM     |  Azure  |
| Domain Controller | Windows Server 2022 - ```D01``` - ```10.0.0.4``` |
| Workstation | Windows Server 2022 - ```CLIENT01``` - ```10.0.0.5``` |
| Domain | ```corplab.local``` |
| Gateway | ```10.0.0.1``` |

***

# Domain Design

```
corplab.local
└── _Branches (OUs)
    ├── Chicago
        ├── Laptops
        ├── Users
        ├── Workstations 
    ├── New York
        ├── Laptops
        ├── Users
        ├── Workstations
    ├── Seattle
        ├── Laptops
        ├── Users
        ├── Workstations
└── _Groups
    ├── Accounting
    ├── Helpdesk
    ├── HR
    ├── ITSupport

```
## Reason for Structure 

**Groups and Branches OUs** allow users to be placed into groups based on their role and then assigned permissions appropriate to that role. This eliminates the confusion that can arise when you assign permissions directly to a user. Branches are created to keep a clean structure as a company grows. 

**Location-based OUs** make it simple and quick to apply Group Policies and delegate access to users across the domain. In a production environment, separating by location rather than object type allows GPOs to be applied to users and computers. It also allows for quicker troubleshooting, a computer or workstations location can be easily found using this structure.

***

# Group Policy Object

## GPO - Password Policy

This GPO is used to enforce password security across the entire domain.

| Policy | Default | New Setting |
| ------ | ------- | ----------  |
| Max password age | 42 days | 60 days |
| Min password length | 7 characters | 10 characters |






