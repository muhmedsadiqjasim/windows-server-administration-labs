# Windows Server Administration Labs

This repository contains two hands-on Windows Server projects focused on Active Directory, Group Policy, server administration, and enterprise infrastructure services.

The projects were built and documented using Windows Server, Windows 11, VMware Workstation, and common Microsoft administration tools.

## Repository Description

Two practical Windows Server administration labs covering Active Directory Domain Services, Group Policy, DNS, DHCP, IIS, file services, printer deployment, Hyper-V Replica, WDS, WSUS, backup, and FSMO role operations.

## Projects Included

### Project 1: Windows Server Domain and Group Policy Lab

Project 1 focuses on building a basic domain environment and applying common Group Policy restrictions and security settings.

Domain used:

```text
muhmedsadiq.local
```

Main server:

```text
Server Name: DC
IP Address: 192.168.100.253
Operating System: Windows Server 2025 Datacenter
```

Client machine:

```text
Client Name: PC-01
IP Address: 192.168.100.50
Operating System: Windows 11 Pro
```

#### Main Tasks

- Created a domain environment named `muhmedsadiq.local`
- Created department OUs for HR, Sales, and IT
- Created users, computers, and department security groups
- Applied a fixed desktop background for domain users
- Hid Programs and Features from Control Panel for HR users
- Removed Properties from This PC context menu
- Disabled external storage for HR and Sales users
- Excluded the HR Manager from the external storage restriction policy
- Removed Task Manager for all users
- Excluded the IT group from the Task Manager restriction
- Configured password and account lockout policies
- Created an HR desktop URL shortcut
- Created a local administrator user named `itadmin`
- Added the IT group as local administrators on domain computers
- Disabled Command Prompt and Run for HR and Sales users
- Allowed ping traffic through Windows Firewall using Group Policy
- Joined Windows 11 client `PC-01` to the domain and tested the policies

---

### Project 2: MCSA Windows Server Enterprise Infrastructure Lab

Project 2 expands the environment into a larger enterprise-style Windows Server infrastructure lab.

Domain used:

```text
company.local
```

Main infrastructure servers:

| Device | Hostname | Role | IP Address |
|---|---|---|---|
| Main Server | PDC | Primary Domain Controller, DNS, DHCP, IIS, File Server, Print Server, Hyper-V | 192.168.50.10 |
| Second Server | ADC-CORE | Additional Domain Controller, DNS, DHCP Failover, IIS, Hyper-V Replica | 192.168.50.11 |
| Nested VM | CORE-VM01 | Windows Server Core VM for Hyper-V Replica testing | 192.168.50.12 |
| Printer | PRN-01 | Shared printer | 192.168.50.30 |
| DHCP Scope | DHCP-SCOPE | Client IP range | 192.168.50.50 - 192.168.50.220 |

#### Main Tasks

- Created the `company.local` domain environment on server `PDC`
- Configured `ADC-CORE` as an additional domain controller using Windows Server Core
- Created department OUs for HR, Sales, Dev, IT, and Finance
- Created Users and Computers sub-OUs for each department
- Created users, computers, and department security groups
- Configured DNS records and DNS round-robin load balancing for `www.company.local`
- Configured password and account lockout policies
- Enabled Remote Desktop using Group Policy
- Enabled Remote Assistance and assigned the IT Support Group as helpers
- Prohibited removable storage, Task Manager, and Control Panel access using Group Policy
- Configured DHCP scope and DHCP failover between PDC and ADC-CORE
- Installed IIS on both servers
- Configured shared folders, mapped drives, quotas, and FSRM restrictions
- Configured a shared printer for all domain users
- Enabled Active Directory Recycle Bin
- Installed Hyper-V and configured Hyper-V Replica
- Configured Windows Server Backup
- Installed and configured Windows Deployment Services
- Tested PXE boot and Windows deployment
- Installed and configured Windows Server Update Services
- Created a GPO to point clients to the WSUS server
- Explained FSMO role transfer and seizure
- Verified the configuration from client machines

## Technologies Used

- Windows Server 2025
- Windows Server Core
- Windows 11 Pro
- VMware Workstation
- Active Directory Domain Services
- Active Directory Users and Computers
- Active Directory Administrative Center
- Group Policy Management
- DNS Server
- DHCP Server
- IIS Web Server
- File Server Resource Manager
- Print Management
- Hyper-V
- Hyper-V Replica
- Windows Server Backup
- Windows Deployment Services
- Windows Server Update Services
- PowerShell

## Skills Practiced

- Windows Server administration
- Domain controller deployment
- Additional domain controller configuration
- Server Core administration
- OU, user, computer, and group management
- Group Policy planning and implementation
- Password and lockout policy configuration
- DNS and DHCP administration
- DHCP failover
- IIS web server setup
- File sharing and storage restrictions
- FSRM quotas and file screening
- Printer deployment
- Active Directory Recycle Bin
- Hyper-V virtualization
- Hyper-V Replica
- Windows backup planning
- PXE boot and OS deployment using WDS
- Patch management using WSUS
- FSMO role management
- Client-side verification and troubleshooting

## Repository Structure

```text
.
├── README.md
├── project-1-domain-gpo-lab/
│   ├── Windows_Server_Project_1.md
│   └── media/
└── project-2-enterprise-infrastructure-lab/
    ├── MCSA_Final_Project.md
    └── media/
```

## Notes

These projects are lab-based and were created for learning and documentation purposes. Some settings, such as disabling Network Level Authentication or using simplified password rules, are suitable for controlled lab environments only and should be reviewed before applying them in production.

## Author

**Muhmedsadiq Ahmed Jasim**

Network Engineering Student  
Interested in System Administration, Windows Server, Linux, and IT Infrastructure
