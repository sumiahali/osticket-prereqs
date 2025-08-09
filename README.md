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

- Windows 11</b> (24H2)

<h2>List of Prerequisites</h2>

- Azure account
- Remote Desktop Connection tool
- Internet access
- [osTicket-Installation-Files.zip](https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD)

<h2>Installation Steps</h2>

1. Create and Connect to Azure VM
- In the **Azure Portal**, start creating a **Windows 11 Virtual Machine**
- During the setup, create a **new Resource Group** for the VM
- Choose a VM size with at least **2 vCPUs** and **16 GiB RAM**
- Choose your own **VM name**, **username**, and **password** (remember for later use)
- Connect to the VM using **Windows App**
<p>
<img width="1294" height="1268" alt="image" src="https://github.com/user-attachments/assets/9a7481ca-8098-4fbf-8d2d-a17a47b423b0" />
</p>
<br />

2. Prepare the Installation Files
- Download the [osTicket-Installation-Files.zip](https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD) onto the VM and extract it to the desktop
- The folder should be called “osTicket-Installation-Files”
- This folder contains all required dependencies and the osTicket installer
<p>
<img width="1618" height="1186" alt="image" src="https://github.com/user-attachments/assets/d9bf92bc-8a12-49f6-9b2f-9d55a918e4cf" />
<img width="1224" height="904" alt="image" src="https://github.com/user-attachments/assets/844e56b1-b8eb-4fab-89a4-bbebe103d085" />
</p>
<br />

3. Install and Configure IIS
- Go to Start menu → Control Panel → Programs 
- Open "Turn Windows features on or off"
- Enable:
  - Internet Information Services (IIS)
  - **CGI** under:
    - *World Wide Web Services → Application Development Features → [✔] CGI*
  <p>
<img width="1276" height="1080" alt="image" src="https://github.com/user-attachments/assets/4f6d353e-8a0a-4f58-b04b-d38d3844a318" />
</p>
<br />

4. Install PHP Manager and Rewrite Module
- From the `osTicket-Installation-Files` folder, install:
  - `PHPManagerForIIS_V1.5.0.msi`
  - `rewrite_amd64_en-US.msi`
 <p>
<img width="1614" height="1182" alt="image" src="https://github.com/user-attachments/assets/50bcf3b9-6f00-41e9-a346-88209385b9b4" />
</p>
<br />

5. Set Up PHP
- Create a new folder: `C:\PHP`
- Extract `php-7.3.8-nts-Win32-VC15-x86.zip` into `C:\PHP`
- Install `VC_redist.x86.exe`
- Open IIS as Administrator
- Register PHP:
  - Go to **PHP Manager** in IIS
  - Select `C:\PHP\php-cgi.exe` as the PHP executable
- Restart IIS (stop and start the server)
<p>
<img width="2126" height="1218" alt="image" src="https://github.com/user-attachments/assets/3bdad123-2bea-4b63-bda4-eeda06ffa3d2" />
<img width="1018" height="436" alt="image" src="https://github.com/user-attachments/assets/6a4672fa-e5bf-4939-8d00-b247ab4c587d" />
<img width="550" height="336" alt="image" src="https://github.com/user-attachments/assets/fc1d47b8-967b-487f-aacf-9b3c3ccc5cb8" />
<img width="550" height="336" alt="image" src="https://github.com/user-attachments/assets/007003ae-531d-4c18-a625-6f6bfa758fb6" />
</p>
<br />

6. Install MySQL
- Install `mysql-5.5.62-win32.msi` from the folder
- Select **Typical Setup**
- After installation, launch the Configuration Wizard:
  - Choose **Standard Configuration**
  - Set username and password (remember/save for later use)
<p>
<img width="998" height="762" alt="image" src="https://github.com/user-attachments/assets/7bf2bb27-bf67-413c-97dd-af74a518790d" />
</p>
<br />

7. Install osTicket
- Extract `osTicket-v1.15.8.zip` from the folder
- Copy the `upload` folder to: `C:\inetpub\wwwroot`
- Rename the folder from `upload` to `osTicket`
- Restart IIS
- In IIS Manager, navigate to: **Sites > Default Web Site > osTicket**
- On the right, click **Browse \*:80** to open osTicket in the browser
<p>
<img width="888" height="326" alt="image" src="https://github.com/user-attachments/assets/bdd7f210-ae04-434b-bab2-33298f32e4ec" />
<img width="1642" height="1148" alt="image" src="https://github.com/user-attachments/assets/a989ef4d-a1a0-4897-b590-83e99dcfd1e5" />
<img width="1646" height="1160" alt="image" src="https://github.com/user-attachments/assets/36b175fc-83ab-4ae6-8755-340d519c5284" />
<img width="2124" height="1222" alt="image" src="https://github.com/user-attachments/assets/fcf6b1d3-8c14-4ac5-bccf-468045788c46" />
<img width="2064" height="1648" alt="image" src="https://github.com/user-attachments/assets/a7078c8a-f44b-4e1b-825b-97fb7e427b3e" />
</p>
<br />

8. Enable Required PHP Extensions
- In IIS, go to **PHP Manager** > “Enable or disable an extension”
- Enable the following:
  - `php_imap.dll`
  - `php_intl.dll`
  - `php_opcache.dll`
- Refresh the browser tab with osTicket to confirm extension errors are gone
<p>
![Uploading image.png…]()

</p>
<br />

9. Configure the osTicket Config File
- Rename the config file:
  - From: `C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php`
  - To: `ost-config.php`
- Right-click `ost-config.php` → Properties → Security
- Disable inheritance and remove all permissions
- Add new permission:
  - User: `Everyone`
  - Permission: Full Control
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

10. Configure the Database Using HeidiSQL
- Install and open HeidiSQL from the folder
- Create a new session with:
  - Username: `root`
  - Password: `root`
- Connect and create a new database:
  - Name: `osTicket`
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

11. Complete osTicket Setup in Browser
- In the osTicket browser installer:
  - Set your Helpdesk Name
  - Set Default Email (for ticket replies)
  - Database Settings:
    - MySQL Database: `osTicket`
    - MySQL Username: `root`
    - MySQL Password: `root`
- Click **Install Now**
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

Final Result
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

- You should see a success message and your new help desk login page:
  - Admin Panel: `http://localhost/osTicket/scp/login.php`
  - End-User Portal: `http://localhost/osTicket/`
<br />
