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

## ⚙️ Detailed Commands

---

### 🔹 1. System Update

```bash
sudo apt update && sudo apt upgrade -y
``
