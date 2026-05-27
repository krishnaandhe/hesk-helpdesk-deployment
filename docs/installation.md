# ⚙️ HESK Installation Guide (Windows vs Linux)

This document provides a **step-by-step deployment guide** for HESK Helpdesk across:

- ✅ Windows Server (IIS + PHP + MySQL)
- ✅ Linux Server (NGINX/Apache + PHP + MySQL)

---

## 📊 Installation Steps (Detailed Comparison)

| Step | Phase                     | Windows (IIS)                                                                 | Linux (NGINX / Apache)                                                  |
|------|--------------------------|------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| 1    | Environment Setup        | Install IIS: <br>`Install-WindowsFeature Web-Server -IncludeManagementTools` | Update system: <br>`sudo apt update && sudo apt upgrade -y`             |
| 2    | Web Server Setup         | Enable CGI: <br>`Install-WindowsFeature Web-CGI`                              | Install NGINX/Apache: <br>`sudo apt install nginx -y`                   |
| 3    | PHP Installation         | Download PHP → Extract to `C:\PHP`                                           | Install PHP: <br>`sudo apt install php php-fpm php-mysql -y`            |
| 4    | PHP Configuration        | Add to PATH: <br>`setx PATH "$($env:PATH);C:\PHP" /M`                         | Edit config: <br>`sudo nano /etc/php/*/fpm/php.ini`                     |
| 5    | DB Installation          | Install MySQL: <br>`winget install MySQL.MySQLServer`                         | Install MariaDB: <br>`sudo apt install mariadb-server -y`               |
| 6    | DB Setup                 | `mysql -u root -p` <br> Create DB/User                                       | `sudo mysql -u root -p` <br> Create DB/User                            |
| 7    | DB Commands              | `CREATE DATABASE hesk_db;` <br>`CREATE USER ...;`<br>`GRANT ALL;`             | Same SQL commands                                                       |
| 8    | phpMyAdmin Setup         | Extract to IIS root                                                          | Install: <br>`sudo apt install phpmyadmin -y`                           |
| 9    | App Deployment           | Copy to: <br>`C:\inetpub\wwwroot\helpdesk`                                   | Copy to: <br>`/var/www/html/helpdesk`                                  |
| 10   | File Copy Command        | `xcopy D:\hesk C:\inetpub\wwwroot\helpdesk /E /I`                             | `sudo cp -r hesk /var/www/html/helpdesk`                                |
| 11   | Permissions Setup        | `icacls helpdesk /grant IIS_IUSRS:(OI)(CI)F /T`                              | `sudo chown -R www-data:www-data /var/www/html/helpdesk`                |
| 12   | Web Access               | `http://localhost/helpdesk`                                                  | `http://server-ip/helpdesk`                                            |
| 13   | Installer Launch         | Open `/install` in browser                                                   | Same                                                                   |
| 14   | Configuration            | Enter DB details, Admin setup                                                | Same                                                                   |
| 15   | Secure Installation      | `Remove-Item helpdesk\install -Recurse`                                      | `sudo rm -rf /var/www/html/helpdesk/install`                            |
| 16   | SSL Setup                | IIS → Bind SSL                                                              | `sudo certbot --nginx`                                                 |
| 17   | Email Setup              | Configure SMTP in `php.ini`                                                  | Configure postfix/sendmail                                             |
| 18   | Backup Setup             | `mysqldump -u root -p hesk_db > C:\backup\hesk.sql`                          | Cron: <br>`mysqldump -u root -p hesk_db > /backup/hesk.sql`            |
| 19   | Monitoring               | IIS Logs, Event Viewer                                                      | `journalctl`, nginx/apache logs                                        |
| 20   | Final Testing            | Test ticket creation                                                        | Test ticket creation                                                   |
| 21   | Go-Live                  | Publish internal URL                                                        | Publish internal URL                                                   |

---

## 📌 Notes

- Windows deployment is ideal for **enterprise MS ecosystem (IIS, AD, M365)**
- Linux deployment is ideal for **scalability and performance**
- Always:
  - ✅ Remove `/install` folder after setup
  - ✅ Enable HTTPS
  - ✅ Backup database regularly

---

## ✅ Recommended Deployment Strategy

| Environment | Recommended OS |
|------------|---------------|
| Enterprise Corporate | Windows + IIS |
| Production / High Scale | Linux + NGINX |
| Testing / Lab | Either |

---

## 🔐 Security Checklist

- ✅ Configure SSL (HTTPS)
- ✅ Restrict database remote access
- ✅ Set strong admin passwords
- ✅ Limit file upload sizes
- ✅ Enable firewall rules

---
``
