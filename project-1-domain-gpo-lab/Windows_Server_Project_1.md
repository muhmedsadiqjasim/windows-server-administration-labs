***In this project I am going to apply these tasks one by one and document every step until the end.  
***

These are the required **tasks** to be accomplished:

- Create a domain environment with domain name “muhmedsadiq.local” Server name: DC and IP Address: 192.168.100.253

- Create a separate OU for each department (HR, Sales, IT).

- Create sample users in each department.

- Create separate groups for each department and add department users to its group.

- Force a fixed background for all domain users.

- Remove Programs and features from the control panel for HR.

- Remove properties from This PC context menu.

- Disable External Storage for HR and Sales Users and exclude the HR manager user.

- Apply remove task manager from all domain users that no policy can allow it and excludes IT team from this policy.

- Configure password policy must change every 90 days, min length 4 digits without complexity, remember the last 2 passwords.

- Force account lock for 60 min after entering 5 wrong passwords.

- Create HR URL for all HR Users on their desktop with Icon for the following link ([<u>http://hrapp.muhmedsadiq.local</u>](https://www.google.com/search?q=http://hrapp.zohdy.local)).

- Using GPO Create a Local admin user (itadmin) and Add domain group IT-Group as a Local Administrator for all domain computers.

- Disable Command Line and Run for HR and Sales.

- Allow ping traffic from Windows Firewall for all computers using Group Policy.

- Join a client machine With Name (PC-01) to domain, IP address (192.168.100.50), and check all above output.

***Note:** in this project I am going to use (Windows Server 2025 Datacenter & Windows 11 Pro) on VMware Workstation, I’m not going to explain how to install these OSs in this project.**  
  
To learn more about installation:***

1.  *Installing VMware:*

[*<u>https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion</u>*](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion)

2.  *Installing Windows Server 2025 on VMware:*

[*<u>https://knowledge.broadcom.com/external/article/371350/installing-windows-server-2025-on-a-vmwa.html</u>*](https://knowledge.broadcom.com/external/article/371350/installing-windows-server-2025-on-a-vmwa.html)

3.  *Installing Windows 11 on VMware*

[*<u>https://knowledge.broadcom.com/external/article/315650/installing-windows-11-as-a-guest-os-on-v.html</u>*](https://knowledge.broadcom.com/external/article/315650/installing-windows-11-as-a-guest-os-on-v.html)

***Table of contents***

**Introduction**

[Virtual Machines Details 2](#virtual-machines-details)

[Creating the Domain Environment 3](#creating-the-domain-environment)

[Active Directory Users and Computers 8](#active-directory-users-and-computers)

[**Group Policy Management (GPM) 10**](#group-policy-management-gpm)

[Fixed Background Policy 10](#fixed-background-policy)

[Adding PC-01 to the Domain 11](#adding-pc-01-to-the-domain)

[Hiding Programs and Features from the Control Panel for HR 13](#hiding-programs-and-features-from-the-control-panel-for-hr)

[Removing Properties from all PCs 14](#removing-properties-from-all-pcs)

[Disabling External Storage for HR and Sales Users and Exclude the HR Manager User 15](#disabling-external-storage-for-hr-and-sales-users-and-exclude-the-hr-manager-user)

[Removing Task Manager from All Users and Excluding the IT Group 17](#removing-task-manager-from-all-users-and-excluding-the-it-group)

[Configuring Password Policy: Change Every 90 Days, Minimum Length 4 Digits Without Complexity, Remember the Last 2 Passwords 19](#configuring-password-policy-change-every-90-days-minimum-length-4-digits-without-complexity-remember-the-last-2-passwords)

[Forcing Account Lock for 60 Minimum After Entering 5 Wrong Passwords 19](#forcing-account-lock-for-60-minimum-after-entering-5-wrong-passwords)

[Creating a URL Shortcut for HR on Desktop 20](#creating-a-url-shortcut-for-hr-on-desktop)

[Creating a Local Admin and a Domain Group as a Local Administrator for All Domain Computers 21](#creating-a-local-admin-and-a-domain-group-as-a-local-administrator-for-all-domain-computers)

[Disabling Command Line and Run for HR and Sales 23](#disabling-command-line-and-run-for-hr-and-sales)

[Allowing Ping Traffic from Windows Firewall for All Computers 25](#allowing-ping-traffic-from-windows-firewall-for-all-computers)

### Virtual Machines Details

**Windows 11 Pro - VM Details:**

<img src="./media/image20.png" style="width:3.2988in;height:3.57757in" />

**Windows Server 2025 Datacenter - VM Details:**

<img src="./media/image38.png" style="width:3.07642in;height:3.28033in" />

**Virtual Network Editor - Details:**<img src="./media/image32.png" style="width:2.80521in;height:2.81526in" />

### Creating the Domain Environment

From the **Server Manager \> Local Server**, I edited **Date and Time**, **IP address** and the **Server name**:

<img src="./media/image46.png" style="width:7.86772in;height:3.58333in" />

*Changing the Time, Date and the Timezone from **Time zone in Local Server**.*

<img src="./media/image5.png" style="width:7.86772in;height:3.58333in" />

*Disabling IPv6 from the **Control Panel \> Network and Internet \> Network Connections.***

*Double-click on **Ethernet0 → Properties → Uncheck: Internet Protocol Version 6 (TCP/IPv6)***

<img src="./media/image28.png" style="width:7.86772in;height:4.09722in" />F*rom the **Control Panel \> Network and Internet \> Network Connections.***

*Double-click on **Ethernet0 → Properties →** Double-click on **Internet Protocol Version 4 (TCP/IPv4)***

| ***IP Address***  | ***192.168.100.253*** |
|-------------------|-----------------------|
| ***Subnet Mask*** | ***255.255.255.0***   |
| ***DNS Server***  | ***192.168.100.253*** |

<img src="./media/image40.png" style="width:5.44063in;height:3.62468in" />

*From **Local Server \> Computer name → Click on Change***

*Write the new **Computer name***

***\*After that you have to restart the server\****

Now I am going to **Add Roles and Features** from the **Manage** in **Server Manager**

<img src="./media/image51.png" style="width:7.86772in;height:3.56944in" /><img src="./media/image33.png" style="width:5.27083in;height:1.15901in" />

<img src="./media/image35.png" style="width:4.3625in;height:3.09131in" /><img src="./media/image4.png" style="width:4.64896in;height:2.65924in" />

Now I am going to set the **Deployment Configuration**. You can check that from the flag icon.

<img src="./media/image42.png" style="width:5.05521in;height:3.71541in" /><img src="./media/image37.png" style="width:5.09688in;height:3.71706in" />

***If you are facing this problem like me, you can solve it easily.***

<img src="./media/image43.png" style="width:5.63854in;height:4.14599in" />

Just go to the **Server Manager → Tools → Computer Management → Local Users and Groups**

Click on **Users →** Right-click on **Administrator**, then set a strong password.

<img src="./media/image19.png" style="width:5.64896in;height:4.03691in" />

***Now the server is ready to be used after restarting.***

### Active Directory Users and Computers

| **No.** | **User / Computer / Group** | **OU** | **Group**     | **Notes**             |
|---------|-----------------------------|--------|---------------|-----------------------|
| 01      | Muhmedsadiq Jasim           | IT     | IT-Group      |                       |
| 02      | Mohammed Ali                | IT     | IT-Group      |                       |
| 03      | Ahmed Hassan                | IT     | IT-Group      |                       |
| 04      | Rand Yassir                 | Sales  | Sales-Group   |                       |
| 05      | Omar Foad                   | Sales  | Sales-Group   |                       |
| 06      | Zahraa Laith                | HR     | HR-Group      | *HR Manager*          |
| 07      | Zaid Rasol                  | HR     | HR-Group      |                       |
| —       | itadmin                     | IT     | IT-Group      | *Local Administrator* |
| 01      | PC-01                       | IT     | Domain Admins | *Main Computer*       |
| 02      | PC-02                       | IT     | IT-Group      |                       |
| 03      | PC-03                       | IT     | IT-Group      |                       |
| 04      | PC-04                       | Sales  | Sales-Group   |                       |
| 05      | PC-05                       | Sales  | Sales-Group   |                       |
| 06      | PC-06                       | HR     | HR-Group      |                       |
| 07      | PC-07                       | HR     | HR-Group      |                       |
| —       | HR-Group                    | Groups |               |                       |
| —       | IT-Group                    | Groups |               |                       |
| —       | Sales-Group                 | Groups |               |                       |

*\*I copy the **Administrator** user from **Users** in **Active Directory Users and Computers** then name it **itadmin** to have the privileges of **Administrator**\**

*I’m not going to explain each step in the **Active Directory Users and Computer** because it is too simple.*

<img src="./media/image48.png" style="width:3.80182in;height:2.60729in" />

<img src="./media/image3.png" style="width:3.81562in;height:2.55401in" />

<img src="./media/image53.png" style="width:3.79479in;height:2.52986in" />

<img src="./media/image24.png" style="width:3.52251in;height:2.35812in" />

# **Group Policy Management (GPM)**

### Fixed Background Policy

***Server Manager \> Tools \> Group Policy Management***

Right click on **muhmedsadiq.local** → Create a new GPO

Right click on **GPO (Wallpaper)** *→ Edit → Go to User Configuration → Administrative Template*

*→ Desktop → Desktop* → Click on Desktop Wallpaper then add the path and enable it.

***Note: before that you have to enable sharing for the Domain Users.***

<img src="./media/image34.png" style="width:4.71146in;height:4.38608in" />

Now I am going to test this policy, but before that we have to update the Group Policy from the Run by using this command: **gpupdate /force**

### Adding PC-01 to the Domain

Now from the PC-01 which is using Windows 11 Pro. I am going to change it from a workgroup to a domain. Before that we have to make sure that the Time and Date, IP address and the name of the device is in the correct way.

<img src="./media/image22.png" style="width:3.71146in;height:2.87176in" />

<img src="./media/image36.png" style="width:5.89896in;height:3.16221in" />

<img src="./media/image29.png" style="width:6.56563in;height:2.88432in" />

***As we can notice the wallpaper has been changed.***

<img src="./media/image54.png" style="width:7.86772in;height:3.55556in" />

### Hiding Programs and Features from the Control Panel for HR

We can apply this by creating a new **GPO** for the **HR OU**.

***User Configuration → Policies → Administrative Template → Control Panel → Programs***

**Enable** → **Hide “Programs and Features” page**

<img src="./media/image7.png" style="width:7.86772in;height:5.625in" /><img src="./media/image45.png" style="width:7.86772in;height:3.56944in" />

### Removing Properties from all PCs

We can apply this by creating a new **GPO** for the whole domain.

***User Configuration → Policies → Administrative Template → Desktop***

**Enable** → **Remove Properties from the Computer icon context menu**

<img src="./media/image30.png" style="width:7.64896in;height:4.56813in" />

<img src="./media/image13.png" style="width:7.86772in;height:3.55556in" />

### Disabling External Storage for HR and Sales Users and Exclude the HR Manager User

We can apply this by creating a new **GPO** for the **HR OU** then **link** the **GPO** to the **Sales OU** and go to ***Delegation*** to **disable** it from the **HR Manager (Zahraa Laith)**.

***User Configuration → Policies → Administrative Template → System → Removable Storage Access***

**Enable *the options below***

<img src="./media/image1.png" style="width:7.86772in;height:4.22222in" />

Adding the ***HR Manager*** from the **Delegation** and **checking Deny** for the **Apply group policy** option.

<img src="./media/image50.png" style="width:4.35196in;height:3.74354in" />

***Zahraa's Account - HR Manager***

<img src="./media/image17.png" style="width:7.86772in;height:3.56944in" />

***Zaid’s Account - HR Employee***

<img src="./media/image18.png" style="width:7.86772in;height:3.59722in" />

### Removing Task Manager from All Users and Excluding the IT Group

We can apply this by creating a new **GPO** for the whole domain and going to ***Delegation*** to **disable** it from the **IT Group**.

***User Configuration → Policies → Administrative Template → System → Ctrl+Alt+Del Options***

**Enable *→ Remove Task Manager***

<img src="./media/image15.png" style="width:4.60708in;height:3.73715in" />

Adding the ***IT Group*** from the **Delegation** and **checking Deny** for the **Apply group policy** option.

<img src="./media/image39.png" style="width:4.59688in;height:4.44291in" />

***Zaid’s Account - HR Employee***

<img src="./media/image14.png" style="width:7.86772in;height:3.51389in" />

***Mohammed’s Account - IT Employee***

<img src="./media/image52.png" style="width:7.86772in;height:3.59722in" />

### Configuring Password Policy: Change Every 90 Days, Minimum Length 4 Digits Without Complexity, Remember the Last 2 Passwords

<img src="./media/image47.png" style="width:7.86772in;height:3.70833in" />

### Forcing Account Lock for 60 Minimum After Entering 5 Wrong Passwords

<img src="./media/image23.png" style="width:7.86772in;height:3.73611in" />

***Computer Configuration → Policies → Windows Settings → Security Settings:***

*→ Password Policy*

*→ Account Lockout Policy*

*This policy is going to be applied for the whole domain.*

### Creating a URL Shortcut for HR on Desktop

We can apply this by creating a new **GPO** for the **HR OU**.

***User Configuration → Preferences → Windows Settings → Shortcuts***

**Right-click → *New Shortcut***

***Then add the below details***

<img src="./media/image6.png" style="width:7.86772in;height:3.83333in" /><img src="./media/image49.png" style="width:7.86772in;height:3.58333in" />

### Creating a Local Admin and a Domain Group as a Local Administrator for All Domain Computers

We can apply this by creating a **GPO** for the whole domain.

***Computer Configuration → Policies → Scripts → Startup → Add***

Then choose the ***.bat file*** which has the script

<img src="./media/image25.png" style="width:7.86772in;height:4.375in" />

**The Script:**

:: ====== Create Local User itadmin ======

net user itadmin P@ssw0rd /add

:: ====== Add itadmin to Local Administrators ======

net localgroup Administrators itadmin /add

:: ====== Add Domain Group IT-Group to Local Administrators ======

net localgroup Administrators “MUHMEDSADIQ\IT-Group”/add

<img src="./media/image27.png" style="width:6.72188in;height:4.76447in" />

<img src="./media/image16.png" style="width:6.70847in;height:4.78922in" />

*We can **verify** that by checking **Computer Management → Local Users and Groups***

### Disabling Command Line and Run for HR and Sales

We can apply this by creating a new **GPO** for the **HR OU** then **link** the **GPO** to the **Sales OU**.

**Disabling CMD  
*User Configuration → Policies → Administrative Template → System***

**Enable *Prevent access to the command prompt***

<img src="./media/image10.png" style="width:3.11771in;height:2.82026in" /><img src="./media/image31.png" style="width:4.07604in;height:2.84483in" />

**Disabling Run**

***User Configuration → Policies → Administrative Template → Start Menu and Taskbar***

**Enable *Remove Run menu from Start menu***

<img src="./media/image2.png" style="width:4.09687in;height:2.92154in" /><img src="./media/image12.png" style="width:3.19062in;height:2.89254in" />

***Checking from Sales - Run***

<img src="./media/image26.png" style="width:7.86772in;height:3.55556in" />

***Checking from Sales - Run***

<img src="./media/image44.png" style="width:7.86772in;height:3.58333in" />

### Allowing Ping Traffic from Windows Firewall for All Computers

We can apply this by creating a **GPO** for the whole domain.

***Computer Configuration → Policies → Windows Settings → Windows Defender Firewall with Advanced Security → Windows Defender Firewall with Advanced Security LDAP → Inbound Rules***

*Right-click **New Rule ***

***Add the rule details like below:***<img src="./media/image41.png" style="width:7.51354in;height:4.07222in" />

<img src="./media/image21.png" style="width:3.7492in;height:3.01674in" /><img src="./media/image8.png" style="width:3.70104in;height:2.98681in" />

***User’s PC***

<img src="./media/image11.png" style="width:7.86772in;height:3.58333in" />

***Pinging from the Server to the User***

### <img src="./media/image9.png" style="width:7.86772in;height:3.56944in" />
