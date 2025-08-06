<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Azure account
- Remote Desktop Connection tool
- Internet access
- `osTicket-Installation-Files.zip`

<h2>Installation Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
1. Create and Connect to Azure VM
- In Microsoft Azure, create a Windows 10 VM with 4 vCPUs  
- Name the VM: `osticket-vm`  
- Use the following credentials:  
  - Username: `labuser`  
  - Password: `osTicketPassword1!`  
- Connect to the VM using Remote Desktop
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
2. Prepare the Installation Files
- Download the `osTicket-Installation-Files.zip` onto the VM and extract it to the desktop  
- This folder contains all required dependencies and the osTicket installer
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
3. Install and Configure IIS
- Open "Turn Windows features on or off"
- Enable:
  - Internet Information Services (IIS)
  - **CGI** under:
    - *World Wide Web Services → Application Development Features → [✔] CGI*
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
4. Install PHP Manager and Rewrite Module
- From the `osTicket-Installation-Files` folder, install:
  - `PHPManagerForIIS_V1.5.0.msi`
  - `rewrite_amd64_en-US.msi`
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
5. Set Up PHP
- Create a new folder: `C:\PHP`
- Extract `php-7.3.8-nts-Win32-VC15-x86.zip` into `C:\PHP`
- Install `VC_redist.x86.exe`
- Open IIS as Administrator
- Register PHP:
  - Go to **PHP Manager** in IIS
  - Select `C:\PHP\php-cgi.exe` as the PHP executable
- Restart IIS (stop and start the server)
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
6. Install MySQL
- Install `mysql-5.5.62-win32.msi` from the folder
- Select **Typical Setup**
- After installation, launch the Configuration Wizard:
  - Choose **Standard Configuration**
  - Set username: `root`
  - Set password: `root`
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
7. Install osTicket
- Extract `osTicket-v1.15.8.zip` from the folder
- Copy the `upload` folder to: `C:\inetpub\wwwroot`
- Rename the folder from `upload` to `osTicket`
- Restart IIS
- In IIS Manager, navigate to: **Sites > Default Web Site > osTicket**
- On the right, click **Browse \*:80** to open osTicket in the browser
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
8. Enable Required PHP Extensions
- In IIS, go to **PHP Manager** > “Enable or disable an extension”
- Enable the following:
  - `php_imap.dll`
  - `php_intl.dll`
  - `php_opcache.dll`
- Refresh the browser tab with osTicket to confirm extension errors are gone
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
9. Configure the osTicket Config File
- Rename the config file:
  - From: `C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php`
  - To: `ost-config.php`
- Right-click `ost-config.php` → Properties → Security
- Disable inheritance and remove all permissions
- Add new permission:
  - User: `Everyone`
  - Permission: Full Control
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
10. Configure the Database Using HeidiSQL
- Install and open HeidiSQL from the folder
- Create a new session with:
  - Username: `root`
  - Password: `root`
- Connect and create a new database:
  - Name: `osTicket`
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
11. Complete osTicket Setup in Browser
- In the osTicket browser installer:
  - Set your Helpdesk Name
  - Set Default Email (for ticket replies)
  - Database Settings:
    - MySQL Database: `osTicket`
    - MySQL Username: `root`
    - MySQL Password: `root`
- Click **Install Now**
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
Final Result

- You should see a success message and your new help desk login page:
  - Admin Panel: `http://localhost/osTicket/scp/login.php`
  - End-User Portal: `http://localhost/osTicket/`
<br />
