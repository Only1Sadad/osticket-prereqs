# osTicket Installation on Azure Virtual Machine (Windows 10)

This guide provides step-by-step instructions to set up **osTicket v1.15.8** on an **Azure Virtual Machine (VM)** running **Windows 10**.

---

## 1. Create and Configure the Azure VM  
- **VM Name:** `osticket-vm`  
- **OS:** Windows 10  
- **vCPUs:** 4  
- **Username:** `labuser`  
- **Password:** `osTicketPassword1!`  
- **Access:** Remote Desktop Connection  

---

## 2. Download and Prepare Installation Files  
Download `osTicket-Installation-Files.zip` inside the VM and extract it to the **Desktop** as `osTicket-Installation-Files`.

---

## 3. Install Required Dependencies  

### Enable IIS with CGI  
Enable **IIS** in Windows and ensure **CGI** is enabled under:  

***World Wide Web Services -> Application Development Features ->CGI***

![IIS CGI Setup](images/iis-cgi-setup.png)  
*Enabling CGI in IIS*  

### Install Required Modules  
- Install **PHP Manager for IIS** (`PHPManagerForIIS_V1.5.0.msi`).  
- Install **Rewrite Module** (`rewrite_amd64_en-US.msi`).  

### Set Up PHP  
1. Create directory: `C:\PHP`  
2. Extract `php-7.3.8-nts-Win32-VC15-x86.zip` to `C:\PHP`  
3. Install **VC++ Redistributable** (`VC_redist.x86.exe`).  

---

## 4. Configure IIS and PHP  
1. Open **IIS as Admin**.  
2. Register PHP: `PHP Manager -> C:\PHP\php-cgi.exe`.  
3. Restart IIS (`Stop` and `Start` the server).  

![PHP Manager Setup](images/php-manager-setup.png)  
*Registering PHP in IIS*  

---

## 5. Install and Configure osTicket  
1. Extract `osTicket-v1.15.8.zip` from `osTicket-Installation-Files`.  
2. Move the `upload` folder to `C:\inetpub\wwwroot\` and rename it to `osTicket`.  
3. Restart IIS.  

### Enable PHP Extensions  
Enable the following extensions in **PHP Manager**:  
- `php_imap.dll`  
- `php_intl.dll`  
- `php_opcache.dll`  

---

## 6. Set Up Database  
1. Install **HeidiSQL**.  
2. Open HeidiSQL and connect (`root/root`).  
3. Create a new database: `osTicket`.  

![Creating Database in HeidiSQL](images/heidisql-create-db.png)  
*Creating the osTicket database in HeidiSQL*  

---

## 7. Complete Installation in Browser  
1. Open `http://localhost/osTicket/scp/login.php` in a browser.  
2. Use the following database details:  
   - **MySQL Database:** `osTicket`  
   - **MySQL Username:** `root`  
   - **MySQL Password:** `root`  
3. Click **Install Now!**  

![osTicket Installation](images/osticket-install.png)  
*osTicket installation in progress*  

---

## 8. Post-Installation Cleanup  
- Delete `C:\inetpub\wwwroot\osTicket\setup`.  
- Set `ost-config.php` to **Read-only**.  

### Access URLs  
- **Admin Panel:** [http://localhost/osTicket/scp/login.php](http://localhost/osTicket/scp/login.php)  
- **End User Portal:** [http://localhost/osTicket/](http://localhost/osTicket/)  

---

## 🎉 Congratulations! osTicket is now installed successfully.

