# ⚙️ HESK Installation Guide (Windows vs Linux)

---

## 📊 Installation Steps (Detailed Comparison)

| Step | Phase               | Windows (IIS)                                                                 | Linux (NGINX / Apache)                                                  |
|------|-------------------|------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| 1    | Environment Setup | Install IIS:<br>`Install-WindowsFeature Web-Server -IncludeManagementTools`  | Update system:<br>`sudo apt update && sudo apt upgrade -y`              |
| 2    | Web Server Setup  | Enable CGI:<br>`Install-WindowsFeature Web-CGI`                              | Install server:<br>`sudo apt install nginx -y`                          |
| 3    | PHP Installation  | Extract PHP to `C:\PHP`                                                      | Install PHP:<br>`sudo apt install php php-fpm php-mysql -y`             |
| 4    | PHP Configuration | Add PATH:<br>`setx PATH "$($env:PATH);C:\PHP" /M`                            | Edit config:<br>`sudo nano /etc/php/*/fpm/php.ini`                     |
| 5    | DB Installation   | Install MySQL:<br>`winget install MySQL.MySQLServer`                         | Install MariaDB:<br>`sudo apt install mariadb-server -y`                |
| 6    | DB Login          | `mysql -u root -p`                                                           | `sudo mysql -u root -p`                                                 |
| 7    | DB Creation       | Create DB & User                                                             | Same SQL commands                                                      |
| 8    | phpMyAdmin Install| Extract to:<br>`C:\inetpub\wwwroot\phpmyadmin`                               | Install:<br>`sudo apt install phpmyadmin -y`                            |
| 9    | phpMyAdmin Config | Edit config:<br>`auth_type = cookie`                                         | Apache symlink:<br>`/var/www/html/phpmyadmin`                          |
| 10   | phpMyAdmin Access | `http://localhost/phpmyadmin`                                                | `http://server-ip/phpmyadmin`                                          |
| 11   | phpMyAdmin Login  | Login with MySQL credentials                                                 | Same                                                                  |
| 12   | Create DB (UI)    | Create `hesk_db` via UI                                                      | Same                                                                  |
| 13   | Create DB User    | Add user & grant privileges                                                  | Same                                                                  |
| 14   | App Deployment    | Copy to:<br>`C:\inetpub\wwwroot\helpdesk`                                    | Copy to:<br>`/var/www/html/helpdesk`                                  |
| 15   | File Copy         | `xcopy D:\hesk C:\inetpub\wwwroot\helpdesk /E /I`                            | `sudo cp -r hesk /var/www/html/helpdesk`                               |
| 16   | Permissions       | `icacls helpdesk /grant IIS_IUSRS:(OI)(CI)F /T`                              | `sudo chown -R www-data:www-data /var/www/html/helpdesk`               |
| 17   | Web Access        | `http://localhost/helpdesk`                                                  | `http://server-ip/helpdesk`                                            |
| 18   | Installer Launch  | Open `/install`                                                              | Same                                                                  |
| 19   | App Setup         | Configure DB + Admin                                                         | Same                                                                  |
| 20   | Security Cleanup  | `Remove-Item helpdesk\install -Recurse`                                      | `sudo rm -rf /var/www/html/helpdesk/install`                           |
| 21   | SSL Setup         | IIS bindings                                                                 | `sudo certbot --nginx`                                                 |
| 22   | Email Setup       | SMTP in `php.ini`                                                            | postfix/sendmail                                                       |
| 23   | Backup Setup      | `mysqldump -u root -p hesk_db > C:\backup\hesk.sql`                          | Cron job backup                                                        |
| 24   | Monitoring        | IIS Logs                                                                     | nginx/apache logs                                                      |
| 25   | Testing           | Create ticket                                                                | Same                                                                  |
| 26   | Go-Live          | Publish URL                                                                  | Publish URL                                                            |

---
``
