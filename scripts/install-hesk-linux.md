# 🐧 HESK Automated Installation – Linux (NGINX / Apache)

---

## 📌 Overview

This document provides a **step-by-step setup of HESK Helpdesk on Linux** using:

- ✅ NGINX / Apache
- ✅ PHP (with required extensions)
- ✅ MySQL / MariaDB
- ✅ phpMyAdmin (optional)

---

## 📊 Installation Steps (Linux)

| Step | Phase               | Linux (NGINX / Apache) Action                         | Explanation                              |
|------|--------------------|------------------------------------------------------|------------------------------------------|
| 1    | System Update      | Update OS packages                                   | Ensures latest security & dependencies   |
| 2    | Web Server Install | Install NGINX or Apache                              | Provides web hosting layer               |
| 3    | PHP Install        | Install PHP & modules                                | Required for HESK execution              |
| 4    | PHP Config         | Modify php.ini                                       | Optimize PHP settings                    |
| 5    | DB Install         | Install MariaDB / MySQL                              | Backend database                         |
| 6    | DB Secure          | Secure database installation                         | Protects DB access                       |
| 7    | DB Setup           | Create database and user                             | Required for HESK                        |
| 8    | phpMyAdmin Install | Install phpMyAdmin (optional)                        | GUI database management                  |
| 9    | HESK Download      | Download latest HESK                                 | Application source                       |
| 10   | HESK Deploy        | Extract to /var/www/html/helpdesk                    | Deploy application                       |
| 11   | Permissions        | Assign web server ownership                          | Required for execution                   |
| 12   | Web Config         | Configure NGINX / Apache                             | Enable PHP handling                      |
| 13   | Restart Services   | Restart web server                                   | Apply changes                            |
| 14   | Run Installer      | Open /helpdesk/install                               | Start web installer                      |
| 15   | Configure HESK     | Enter DB and admin details                           | Setup application                        |
| 16   | Remove Installer   | Delete /install folder                               | Security step                            |
| 17   | Enable SSL         | Setup HTTPS with certbot                             | Secure communication                     |
| 18   | Backup Setup       | Configure DB backup                                  | Data protection                          |
| 19   | Testing            | Create test ticket                                   | Validate deployment                      |
| 20   | Go-Live           | Publish system URL                                   | Production deployment                    |

---

# ⚙️ Detailed Installation Commands

---

### 🔹Step 1. System Update

```bash
sudo apt update && sudo apt upgrade -y
```
---
### 🔹Step 2. Install Web Server
✅ NGINX
```
sudo apt install nginx -y
``
---
✅ Apache
```
sudo apt install apache2 -y
```
---
✔ Installs web server for hosting HESK
```
---
### 🔹 Step 3: Install PHP (Compatible Version)
```bash
sudo apt install php php-fpm php-mysql php-cli php-curl php-gd php-zip php-mbstring -y
``
Verify:
php -v
✔ PHP 8.1 / 8.2 recommended

### 🔹 Step 4: Install MariaDB
```bash
sudo apt install mariadb-server -y
Secure installation:
sudo mysql_secure_installation
``
✔ Protects DB with password & security policies

### Step 5: Create Database & User
sudo mysql -u root -p
``
CREATE DATABASE hesk_db;
CREATE USER 'hesk_user'@'localhost' IDENTIFIED BY 'StrongPassword';
GRANT ALL PRIVILEGES ON hesk_db.* TO 'hesk_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;

✔ Prepares database for HESK

### 🔹 Step 6: Install phpMyAdmin (Optional)
```bash
sudo apt install phpmyadmin -y
``
Apache Integration:
sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin
sudo systemctl restart apache2

Access:
http://server-ip/phpmyadmin
✔ Simplifies DB management

### 🔹 Step 7: Download HESK
```
cd /var/www/html
sudo mkdir helpdesk
cd helpdesk
sudo wget https://www.hesk.com/files/hesk.zip
``
✔ Downloads official HESK package

### 🔹 Step 8: Extract HESK
```
sudo apt install unzip -y
sudo unzip hesk.zip
``
✔ Extracts application files

### 🔹 Step 9: Set Permissions
sudo chown -R www-data:www-data /var/www/html/helpdesk
sudo chmod -R 755 /var/www/html/helpdesk
✔ Ensures web server access

### 🔹 Step 10: Configure Web Server
✅ NGINX
sudo nano /etc/nginx/sites-available/helpdesk

```
server {
    listen 80;
    root /var/www/html/helpdesk;
    index index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php-fpm.sock;
    }
}
```
Enable:
sudo ln -s /etc/nginx/sites-available/helpdesk /etc/nginx/sites-enabled/
sudo systemctl restart nginx

✅ Apache
sudo a2enmod php
sudo systemctl restart apache2

✔ Enables PHP execution

### 🔹 Step 11: Run Installer
Open browser:
http://server-ip/helpdesk/install

✔ Complete setup wizard

### 🔹 Step 12: Secure Installation
sudo rm -rf /var/www/html/helpdesk/install

✔ Prevents reinstallation attacks

###🔹 Step 13: Enable SSL (HTTPS)
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx
✔ Secures traffic

### 🔹 Step 14: Setup Backup
crontab -e

Add:
0 2 * * * mysqldump -u root -pYourPassword hesk_db > /backup/hesk.sql
``
✔ Automates daily backup
```
### 🔹 Step 15: Testing
-Open UI
-Create ticket
-Verify DB entry
-Check logs

✔ Confirms full functionality
```
🔐 Security Best Practices
-✅ Enable HTTPS (SSL)
-✅ Restrict phpMyAdmin access
-✅ Disable root remote login
-✅ Use strong passwords
-✅ Schedule backups

✅ Summary
This setup ensures:
-Secure deployment
-Scalable architecture
-High performance
-Production readiness












