
# osTicket Installation Guide

This guide covers the prerequisites and installation of the open-source help desk ticketing system, osTicket.

![osTicket logo](https://i.imgur.com/Clzj7Xs.png)

## **Table of Contents**
1. [Environments and Technologies Used](#environments-and-technologies-used)
2. [Operating Systems Used](#operating-systems-used)
3. [Prerequisites](#prerequisites)
4. [Installation Steps](#installation-steps)

---

## **Environments and Technologies Used**
- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

## **Operating Systems Used**
- Windows 10 (21H2)

## **Prerequisites**
- Azure Virtual Machine
- Internet Information Services (IIS)
- PHP Manager
- Rewrite Module
- VC Redist
- MySQL
- Heidi SQL
- osTicket v1.15.8

[**Download Link**](https://drive.google.com/drive/u/0/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6)

---

## **Installation Steps**

1. **Setup Virtual Machine on Azure**:
   - Go to [Azure Portal](https://portal.azure.com/).
   - Setup your virtual machine with Windows 10 Pro, version 22H2. Note: Ensure your VM has at least 2 vCPUs and 16 GBs of memory.
   - Connect using the public IP address via the remote desktop connection app.

     ![VM Connection](https://imgur.com/MAhXK2e.png)

2. **Configure Windows Features**:
   - On your VM, navigate to the control panel > programs > Turn Windows features on and off.

     ![Windows Features](https://imgur.com/fGXMpx4.png)

3. **Install IIS with CGI and Common HTTP Features**:
   - World Wide Web Services -> Application Development Features ->
     - [X] CGI
     - [X] Common HTTP Features

     ![IIS Features](https://imgur.com/LQjw9le.png)

     > **Note**: Ensure all Common HTTP Features are checked.

4. **Test IIS Installation**:
   - In a browser, navigate to `127.0.0.1`.

     ![IIS Browser Test](https://imgur.com/eICujoq.png)

5. **Setup PHP and Required Modules**:
   - From Installation Files:
     1. Install PHP Manager for IIS (`PHPManagerForIIS_V1.5.0.msi`).
     2. Install Rewrite Module (`rewrite_amd64_en-US.msi`).
     3. Create a folder in the C drive named `PHP`.
     4. Download and unzip PHP 7.3.8 (`php-7.3.88-nts-Win32-VC15-x866.zip`) to `C:\PHP`.

     > **Attention**: If a warning appears, choose to "Keep" the file.

6. **Install VC Redist**:
   - Download and install `VC_redist.x86.exe` from the installation files.

7. **Setup MySQL**:
   - Download and install MySQL 5.5.62 (`mysql-5.5.62-win32.msi`).
   - Follow the setup wizard: Typical Setup -> Launch Configuration Wizard (after install) -> Standard Configuration.
   - Set the root password as `Password1` and execute the process.

8. **Configure IIS for PHP**:
   - Search for IIS in the windows search bar. Open IIS as an administrator.
   - Register a new PHP version within IIS pointing to the `php-cgi.exe` file located in `C:\PHP`.
   - Restart the IIS server.

9. **Install osTicket**:
   - Download osTicket from the Installation Files Folder.
   - Extract and copy the "upload" folder to `c:\inetpub\wwwroot`.
   - Rename the folder from "upload" to "osTicket" within `c:\inetpub\root`.
   - Reload IIS.

10. **Enable Required Extensions in osTicket**:
    - In IIS, navigate to sites -> Default -> osTicket.
    - Open PHP manager and enable the following extensions:
      - `php_imap.dll`
      - `php_intl.dll`
      - `php_opcache.dll`

11. **Database Configuration**:
    - Download and install HeidiSQL from the Installation Files.
    - Create a new session ensuring the username is `root` and the password is `Password1`.
    - Create a new database named `osTicket` within HeidiSQL.
    - Back in the osTicket setup on your browser, fill out the form, setting the database name as `osTicket` and using the credentials `root` and `Password1`.

12. **Post Installation Configurations**:
    - Delete the setup folder located in `C:\inetpub\wwwroot\osTicket\setup`.
    - Set the permissions of the `ost-config.php` file back to "Read" only.
    - Log in to osTicket through the browser.

     ![osTicket Login](https://imgur.com/uHVdDsx.png)

---

**Congratulations!** osTicket is now successfully installed and configured on your system!
