# 🏗️ HESK Architecture Overview

## 🧩 Components

- Web Server: IIS / Apache / NGINX
- Application Layer: HESK (PHP)
- Database: MySQL / MariaDB
- Admin Interface: PHPMyAdmin
- Storage: Attachments & Logs

---

## 🔄 Flow

User → Web Server → PHP → HESK → Database → Response

---

## 🌐 Deployment Models

### ✅ Windows Stack
- Windows Server 2022
- IIS + PHP
- MySQL / MariaDB
- phpMyAdmin

### ✅ Linux Stack
- Ubuntu / CentOS
- NGINX / Apache
- PHP-FPM
- MySQL / MariaDB
- phpMyAdmin

---

## 🔐 Security Layers

- HTTPS (SSL)
- Firewall Rules
- Role-based access control
- DB backup strategy
