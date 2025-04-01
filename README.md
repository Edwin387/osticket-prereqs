 
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

- Windows 10</b> (22H2)

<h2>List of Prerequisites</h2>

- Microsoft Azure Account
- Basic knowledge of IIS
- Remote Desktop access
- osTicket installation files
- HeidiSQL

<h2>Installation Steps</h2>
        
<h3>1.) Creating a Virtual Machine</h3>

In Microsoft Azure, we will create a VM and add it to a new Resource Group, titled "osTicket".

- **VM Name:** osticket-vm
- **Image:** Windows 10 Pro, version 22H2 - x64 Gen2
- **Size:** 2 vCPUs, 8 GiB Memory

Check the licensing box, review the VM, and create it. No changes are needed for the management, disks, or networking sections.

![image alt](https://github.com/Edwin387/osticket-prereqs/blob/main/shot%2029.PNG?raw=true)

![image alt](https://github.com/Edwin387/osticket-prereqs/blob/main/shot%2030.PNG?raw=true)



<h3>2.) Accessing the Virtual Machine</h3>

- Log into the VM using **Remote Desktop** with the credentials created during the VM setup. 

![image](https://github.com/user-attachments/assets/89a075d3-dbe9-4489-b31a-0f5a5f648919)


<h3>3.) Download and Prepare Installation Files</h3>

- Within the VM, download the `osTicket-Installation-Files.zip` and unzip it to your desktop.
- The folder should be named `osTicket-Installation-Files`.

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/Screenshot%203.PNG?raw=true) 


<h3>4.) Install IIS and Enable Required Features</h3>

- Open **Control Panel** -> **Programs** -> **Turn Windows features on or off**.
- Install/enable **IIS** with the following features:
  - **Internet Information Services** -> **World Wide Web Services** -> **Application Development Features** -> [X] CGI

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/shot%204.PNG?raw=true)

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/Screenshot%201.PNG?raw=true)

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/Screenshot%202.PNG?raw=true)

<h3>5.) Install Required Components</h3>

- From the `osTicket-Installation-Files` folder:
  - Install **PHP Manager for IIS**: `PHPManagerForIIS_V1.5.0.msi`.
  - Install **Rewrite Module**: `rewrite_amd64_en-US.msi`.
 
![image](https://github.com/Edwin387/osticket-prereqs/blob/main/shot%208.PNG?raw=true)

<h3>6.) Setup PHP</h3>

- Create the directory `C:\PHP`.
- Unzip `PHP 7.3.8` (`php-7.3.8-nts-Win32-VC15-x86.zip`) into the `C:\PHP` folder.
- Install `VC_redist.x86.exe`.

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/shot%2032.PNG?raw=true)

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/shot%208.PNG?raw=true)

<h3>7.) Install MySQL</h3>

- From the `osTicket-Installation-Files` folder, install MySQL 5.5.62 (`mysql-5.5.62-win32.msi`).
  - Select **Typical Setup**.
  - Launch the Configuration Wizard:
    - **Standard Configuration**
    - Input a username and password, don't forget this!

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/shot%209.PNG?raw=true)

<h3>8.) Configure IIS</h3>

- Open IIS as an administrator.
- Register PHP:
  - Go to **PHP Manager** -> Register PHP path -> `C:\PHP\php-cgi.exe`.
- Reload IIS (Stop and Start the server).

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/shot%2033.PNG?raw=true)

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/shot%2010.PNG?raw=true)

<h3>9.) Install osTicket</h3>

- From the `osTicket-Installation-Files` folder:
  - Unzip `osTicket-v1.15.8.zip`.
  - Copy the `upload` folder into `C:\inetpub\wwwroot`.
  - Rename the `upload` folder to `osTicket`.

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/shot%2034.PNG?raw=true)

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/shot%2012.PNG?raw=true)

<h3>10.) Configure osTicket</h3>

- Open IIS:
  - Navigate to **Sites** -> **Default** -> **osTicket**.
  - On the right, click **Browse *:80**.

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/shot%2014.PNG?raw=true)

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/shot%2015.PNG?raw=true)

- Note extensions that are not enabled. Go back to IIS:
  - Navigate to **Sites** -> **Default** -> **osTicket**.
  - Double-click **PHP Manager** -> Click **Enable or disable an extension**.
  - Enable the following extensions:
    - `php_imap.dll`
    - `php_intl.dll`
    - `php_opcache.dll`

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/shot%2016.PNG?raw=true)

<h3>11.) Update Configuration Files</h3>

- Rename `ost-config.php`:
  - From: `C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php`
  - To: `C:\inetpub\wwwroot\osTicket\include\ost-config.php`.
- Assign Permissions by clicking on `properties` on ost-config.php -> click on security -> click on advanced security settings.
  - Disable inheritance -> Remove all permissions.
  - Add new permissions -> **Everyone** -> **Full control** -> **Apply**

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/shot%2017.PNG?raw=true)

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/shot%2018.PNG?raw=true)

<h3>12.) Complete osTicket Setup</h3>

- In the browser, continue the osTicket setup:
  - Set **Helpdesk Name**.
  - Set **Default email** (receives emails from customers).

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/shot%2019.PNG?raw=true)

<h3>13.) Install HeidiSQL and Configure Database</h3>

- From the `osTicket-Installation-Files` folder, install **HeidiSQL**.
- Open HeidiSQL:
  - Create a new session: **Username:** root / **Password:** root.
  - Connect to the session.
  - Create a database named `osTicket`.

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/shot%2020.PNG?raw=true)

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/shot%2021.PNG?raw=true)

<h3>14.) Finalize osTicket Installation</h3>

- In the browser, complete the setup:
  - **MySQL Database:** osTicket  
  - **MySQL Username:** root  
  - **MySQL Password:** root  
- Click **Install Now!**

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/68747470733a2f2f692e696d6775722e636f6d2f6e69714f706f592e706e67%20(2).png?raw=true)

<h3>15.) Verify Installation</h3>

- Access your help desk login page: `http://localhost/osTicket/scp/login.php`.

![image](https://github.com/Edwin387/osticket-prereqs/blob/main/shot%2035.PNG?raw=true)

<h2>Conclusion</h2>

Congratulations! You have successfully installed and configured osTicket on your virtual machine. Your help desk system is now ready to use!

<br />
