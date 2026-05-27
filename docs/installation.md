# ⚙️ HESK Installation Guide (Windows vs Linux)

---

## 📊 Installation Steps (Detailed Comparison)

| Step | Phase                | Windows (IIS)                                                                 | Linux (NGINX / Apache)                                                  |
|------|---------------------|------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| 1    | Environment Setup   | Install IIS:<br>`Install-WindowsFeature Web-Server -IncludeManagementTools`  | Update system:<br>`sudo apt update && sudo apt upgrade -y`              |
| 2    | Web Server Setup    | Enable CGI:<br>`Install-WindowsFeature Web-CGI`                              | Install Web Server:<br>`sudo apt install nginx -y`                      |
| 3    | PHP Installation    | Download PHP → Extract to `C:\PHP`                                           | Install PHP:<br>`sudo apt install php php-fpm php-mysql -y`             |
| 4    | PHP Configuration   | Add PATH:<br>`setx PATH "$($env:PATH);C:\PHP" /M`                            | Configure PHP:<br>`sudo nano /etc/php/*/fpm/php.ini`                   |
| 5    | DB Installation     | Install MySQL:<br>`winget install MySQL.MySQLServer`                         | Install MariaDB:<br>`sudo apt install mariadb-server -y`                |
| 6    | DB Setup            | Login:<br>`mysql -u root -p`                                                 | Login:<br>`sudo mysql -u root -p`                                      |
| 7    | DB Commands         | `CREATE DATABASE hesk_db;`<br>`CREATE USER ...;`<br>`GRANT ALL;`              | Same SQL commands                                                       |

| 8.1  | phpMyAdmin Install  | Download ZIP → Extract to:<br>`C:\inetpub\wwwroot\phpmyadmin`               | Install package:<br>`sudo apt install phpmyadmin -y`                    |
| 8.2  | phpMyAdmin Config   | Rename:<br>`config.sample.inc.php → config.inc.php`<br>Edit file:<br>`$cfg['auth_type']='cookie';` | Apache:<br>`sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin`<br>NGINX: Configure site block |
| 8.3  | phpMyAdmin Access   | Open:<br>`http://localhost/phpmyadmin`                                       | Open:<br>`http://server-ip/phpmyadmin`                                 |
| 8.4  | phpMyAdmin Login    | Username:<br>`root`<br>Password:<br>`MySQL password`                         | Same credentials                                                        |
| 8.5  | Create Database     | UI → New → `hesk_db`                                                         | Same via UI                                                             |
| 8.6  | Create DB User      | User Accounts → Add User → Grant All Privileges                             | Same via UI                                                             |

| 9    | App Deployment      | Copy to:<br>`C:\inetpub\wwwroot\helpdesk`                                   | Copy to:<br>`/var/www/html/helpdesk`                                   |
| 10   | File Copy          | `xcopy D:\hesk C:\inetpub\wwwroot\helpdesk /E /I`                           | `sudo cp -r hesk /var/www/html/helpdesk`                               |
| 11   | Permissions Setup   | `icacls helpdesk /grant IIS_IUSRS:(OI)(CI)F /T`                            | `sudo chown -R www-data:www-data /var/www/html/helpdesk`               |
| 12   | Web Access         | `http://localhost/helpdesk`                                                 | `http://server-ip/helpdesk`                                            |
| 13   | Installer Launch   | Open `/install`                                                             | Same                                                                   |
| 14   | App Config         | Enter DB details + Admin setup                                              | Same                                                                   |
| 15   | Secure Setup       | `Remove-Item helpdesk\install -Recurse`                                     | `sudo rm -rf /var/www/html/helpdesk/install`                           |
| 16   | SSL Setup          | Configure in IIS bindings                                                   | `sudo certbot --nginx`                                                 |
| 17   | Email Setup        | SMTP config in `php.ini`                                                    | Use postfix/sendmail                                                   |
| 18   | Backup Setup       | `mysqldump -u root -p hesk_db > C:\backup\hesk.sql`                         | Cron job:<br>`mysqldump -u root -p hesk_db > /backup/hesk.sql`        |
| 19   | Monitoring         | IIS Logs / Event Viewer                                                     | `journalctl`, nginx/apache logs                                        |
| 20   | Final Testing      | Create test ticket                                                          | Create test ticket                                                     |
| 21   | Go-Live           | Publish helpdesk URL                                                        | Publish helpdesk URL                                                   |

---

## 📌 Notes

- ✅ Windows → Best for enterprise Microsoft environments  
- ✅ Linux → Best for performance & scalability  
- ✅ phpMyAdmin simplifies DB setup (optional but recommended)  

---

## 🔐 Security Checklist

- ✅ Remove `/install` folder  
- ✅ Enable HTTPS  
- ✅ Restrict phpMyAdmin access (IP/Firewall)  
- ✅ Use strong DB credentials  
- ✅ Regular backups  

---
