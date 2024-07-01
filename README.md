# SIEM-Honeynet
## Overview

This project involves setting up Windows and Linux virtual machines (VMs), configuring security rules, disabling firewalls, installing SQL Server, creating attack scenarios, and monitoring logs. Additionally, Azure Active Directory (AAD) and Microsoft Sentinel are configured for enhanced security monitoring.

## Project Steps

1. **Creating VMs and Configuring Security Rules**
    - Created Windows and Linux VMs.
    - Opened up security rules to allow all inbound traffic.

    ![VM Security Rules](path_to_screenshot1)

2. **Disabling Windows Firewall**
    - Disabled Windows firewall to make the VM accessible by the public.

    ![Disabled Firewall](path_to_screenshot2)

3. **Installing SQL Server and SQL Server Management Studio**
    - Installed SQL Server 2019 and SQL Server Management Studio.
    - Configured SQL audit events to be written to the security logs.
    - Granted Event Viewer access to the SQL server through the Windows registry.

    ![SQL Server Installation](path_to_screenshot3)

4. **Configuring Audit Policy**
    - Used the command line to configure the audit policy to generate SQL logs within the application logs in Event Viewer.

    ![Audit Policy Configuration](path_to_screenshot4)

5. **Creating Attack Scenarios**
    - Created an attack VM and attempted to RDP into the other Windows VM with incorrect credentials.
    - Installed SQL management on the attack VM and attempted to log into the SQL server to create logs.
    - Created failed login attempts for the Linux VM by attempting to SSH into the Linux VM with a fake user and incorrect password.

    ![Attack Scenarios](path_to_screenshot5)

6. **Reviewing Logs**
    - Reviewed logs in Event Viewer (security and application).
    - Let the VMs run for a day to see if any attacks or login attempts occurred.
    - Logged into the Linux VM via SSH to see the failed login attempts from earlier.

    ![Log Review](path_to_screenshot6)

7. **Configuring Azure Active Directory**
    - Created new users at different levels:
        - Tenant-Level Global Reader
        - Subscription-Level Privileges
        - Resource Group Level Contributor

    ```text
    User: globalreaderjohn@Hunchojack01outlook.onmicrosoft.com
    Display Name: Greaderjohn
    Password: Cyberlab123!

    User: subreaderjane@Hunchojack01outlook.onmicrosoft.com
    Display Name: Sreaderjane
    Password: Voxo406707
    Cyberlab123!

    User: rgcontributordave@Hunchojack01outlook.onmicrosoft.com
    Display Name: Drgcontributor
    Password: Suda685152
    Cyberlab123!
    ```

    ![AAD Configuration](path_to_screenshot7)

8. **Creating Log Analytics Workspace and Microsoft Sentinel**
    - Created a Log Analytics workspace.
    - Connected Microsoft Sentinel with the Log Analytics workspace.
    - Created a new watchlist to consist of data gathered from "Attacks".

    ```text
    Watchlist Name/Alias: geoip
    Source Type: Local File
    Number of Lines Before Row: 0
    Search Key: network
    ```

    ![Log Analytics Workspace](path_to_screenshot8)

9. **Enabling Microsoft Defender for Cloud**
    - Enabled Microsoft Defender for Cloud and connected it to the cloud analytics workspace.
    - Configured flow logs for both VMs.

    ![Defender for Cloud](path_to_screenshot9)

10. **Creating Data Collection Rules**
    - Configured Linux Syslogs to only send the LOG_AUTH information to Azure Monitor Logs.
    - Configured a data collection rule for the Windows VM to aggregate information logs from the application and audit success and failure for security.
    - Added XPath queries to create logs when the VM discovers malware and to forward firewall logs if there is any tampering.

    ![Data Collection Rules](path_to_screenshot10)

11. **Setting Up Azure Active Directory (Entra) Diagnostics**
    - Created a diagnostic setting to track sign-in activities.
    - Created a user with global admin permissions, logged in, assigned the role of Global Administrator, then deleted the user to observe audit logs.

    ```text
    Dummy User: dummy_user@Hunchojack01outlook.onmicrosoft.com
    Password: Fosa677334
              Cyberlab123!
    ```

    ![AAD Diagnostics](path_to_screenshot11)

## Conclusion
