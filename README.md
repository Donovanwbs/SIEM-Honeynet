# SIEM-Honeynet
## Overview

This project involves setting up Windows and Linux virtual machines (VMs), configuring security rules, disabling firewalls, installing SQL Server, creating attack scenarios, and monitoring logs. Additionally, Azure Active Directory (AAD) and Microsoft Sentinel are configured for enhanced security monitoring.

## Project Steps

1. **Creating VMs and Configuring Security Rules**
    - Created Windows and Linux VMs.
    - Opened up security rules to allow all inbound traffic.

    [ Security Rules]
   
   <img width="793" alt="image" src="https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/caca107b-a6cd-444a-a132-96fba41768e0">

    [ Security Rules]

   <img width="794" alt="image" src="https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/5388f9be-cfa3-4409-8795-1fc6eb27d366">



3. **Disabling Windows Firewall**
    - Disabled Windows firewall to make the VM accessible by the public.

    [Disabled Firewall]

   <img width="782" alt="image" src="https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/262d4236-6b7b-4a9e-8b28-fb579d41dba7">

5. **Installing SQL Server and SQL Server Management Studio**
    - Installed SQL Server 2019 and SQL Server Management Studio.
    - Configured SQL audit events to be written to the security logs.
    - Through the windows registry I was able to grant  event viewer access to the SQL server so that logs will generate with in event viewer 

    [Granted Event Viewer access to the SQL server through the Windows registry]
   
    <img width="716" alt="image" src="https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/f9e4046b-7704-4485-a9dd-0c7fef98fb52">

      Source: https://learn.microsoft.com/en-us/sql/relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log?view=sql-server-ver16

7. **Configuring Audit Policy**
    - Used the command line to configure the audit policy to generate SQL logs within the application logs in Event Viewer.

    [Audit Policy Configuration]

   (<img width="492" alt="image" src="https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/dc07d02f-2064-46c0-ab13-402191a659cf">)

9. **Creating Attack Scenarios**
    - Created an attack VM and attempted to RDP into the other Windows VM with incorrect credentials.
    - Installed SQL management on the attack VM and attempted to log into the SQL server to create logs.
    - Created failed login attempts for the Linux VM by attempting to SSH into the Linux VM with a fake user and incorrect password.

    [Attack Scenarios]

   <img width="428" alt="image" src="https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/9a955484-92bf-4675-a733-d10989090a2c">

11. **Reviewing Logs**
    - Reviewed logs in Event Viewer (security and application).
    - Let the VMs run for a day to see if any attacks or login attempts occurred.
    - Logged into the Linux VM via SSH to see the failed login attempts from earlier.

    [Log Review]
    
    <img width="599" alt="image" src="https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/8e3d89ef-1267-4505-9a0c-01502c2e5a6b">

13. **Configuring Azure Active Directory**
    - Created new users at different levels:
        - Tenant-Level Global Reader
        - Subscription-Level Privileges
        - Resource Group Level Contributor

    <img width="953" alt="image" src="https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/14e3c67e-e88e-4d13-8f63-9b5f86cd500a">

    <img width="475" alt="image" src="https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/659e4c62-a3b2-4994-84c4-a3b6b60b9249">

    <img width="383" alt="image" src="https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/ea6ed588-9365-4d74-bea0-a6a7e66ab7c1">

    <img width="473" alt="image" src="https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/0b60876d-46d5-4d4a-8713-02fc7604b41c">


    
13. **Creating Log Analytics Workspace and Microsoft Sentinel**
    - Created a Log Analytics workspace.
    - Connected Microsoft Sentinel with the Log Analytics workspace.
    - Created a new watchlist to consist of data gathered from "Attacks".

    ```text
    Watchlist Name/Alias: geoip
    Source Type: Local File
    Number of Lines Before Row: 0
    Search Key: network
    ```

    <img width="479" alt="image" src="https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/3340dea6-049a-42ec-a40c-8b449f0111f5">

    <img width="476" alt="image" src="https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/1aac8a93-95c8-4b3d-9293-8215f7faedfd">

    <img width="455" alt="image" src="https://github.com/Don1914/SIEM-Honeynet/assets/84741902/c60b60dc-6b43-4f3f-bbe4-ccc2f9594e84">


14. **Enabling Microsoft Defender for Cloud**
    - Enabled Microsoft Defender for Cloud and connected it to the cloud analytics workspace.
    - Configured flow logs for both VMs.

    <img width="803" alt="image" src="https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/42c45df2-94d1-4e4d-88b4-d5b9eba842bb">

    <img width="953" alt="image" src="https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/07bf63db-8841-4480-8dd3-9ec12ed676a9">

    <img width="918" alt="image" src="https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/10ca765e-6394-4c84-a8a8-eb522881e30c">

    <img width="929" alt="image" src="https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/a3064a40-c065-4f00-88c1-d8294510bd04">

15. **Creating Data Collection Rules**
    - Configured Linux Syslogs to only send the LOG_AUTH information to Azure Monitor Logs.
    - Configured a data collection rule for the Windows VM to aggregate information logs from the application and audit success and failure for security.
    - Added XPath queries to create logs when the VM discovers malware and to forward firewall logs if there is any tampering.

    <img width="437" alt="image" src="https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/5d2af999-ba28-4d32-8881-12a584b6540e">


16. **Setting Up Azure Active Directory (Entra) Diagnostics**
    - Created a diagnostic setting to track sign-in activities.
    - Created a user with global admin permissions, logged in, assigned the role of Global Administrator, then deleted the user to observe audit logs.



    <img width="470" alt="image" src="https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/eb92b607-9354-42be-bb60-fe562d43ba3f">

    ![image](https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/8724dd14-aebb-4d32-8474-6ce537d5a917)

    ![image](https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/90c5389f-e0cf-4b9a-888d-426bd76e1a20)

    ![image](https://github.com/Donovanwbs/SIEM-Honeynet/assets/84741902/4a5b545a-b531-4fe9-9199-c8ef8236415f)


## STILL IN PROGRESS!!!
