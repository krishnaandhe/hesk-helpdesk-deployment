# ⚙️ HESK Installation Steps (Windows vs Linux)

## 📌 Deployment Modes Supported

- ✅ Windows Enterprise Deployment (IIS + PHP)
- ✅ Linux Production Deployment (NGINX / Apache + PHP-FPM)

| Step | Phase                     | Windows (IIS)                                                                 | Linux (NGINX / Apache)                                                  |
|------|--------------------------|------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| 1    | Environment Setup        | Install Windows Server & enable IIS Role                                     | Install Ubuntu/CentOS & update system                                  |
| 2    | Web Server Setup         | Enable IIS + CGI                                                             | Install NGINX / Apache                                                  |
| 3    | PHP Installation         | Install PHP for Windows + configure in IIS                                   | Install PHP + PHP-FPM                                                   |
| 4    | PHP Configuration        | Configure handler mapping in IIS                                             | Configure php.ini & PHP-FPM settings                                   |
| 5    | Database Installation    | Install MySQL / MariaDB                                                      | Install MySQL / MariaDB                                                |
| 6    | DB Management Tool       | Install phpMyAdmin (Optional via IIS)                                        | Install phpMyAdmin via package manager                                 |
| 7    | Database Setup           | Create DB using phpMyAdmin or MySQL CLI                                      | Create DB using MySQL CLI or phpMyAdmin                                |
| 8    | Application Deployment   | Copy HESK files to C:\inetpub\wwwroot\helpdesk                               | Copy HESK files to /var/www/html/helpdesk                              |
| 9    | Permissions Setup        | Configure NTFS permissions for IIS_IUSRS                                     | Set ownership: www-data / apache user                                  |
| 10   | Web Access               | Access via http://server-ip/helpdesk                                         | Access via http://server-ip/helpdesk                                   |
| 11   | Installation Wizard      | Run browser installation (IIS hosting)                                       | Run browser installation (NGINX/Apache hosting)                        |
| 12   | Database Configuration   | Enter DB credentials (MySQL on Windows)                                      | Enter DB credentials (MySQL on Linux)                                  |
| 13   | Application Setup        | Complete HESK setup steps                                                    | Complete HESK setup steps                                              |
| 14   | Security Hardening       | Enable SSL in IIS + remove /install folder                                   | Enable SSL (Let's Encrypt) + remove /install folder                    |
| 15   | Email Integration        | Configure SMTP via IIS/PHP                                                   | Configure SMTP via postfix/sendmail                                   |
| 16   | Final Configuration      | Setup departments, roles, and categories                                     | Setup departments, roles, and categories                               |
| 17   | Testing & Validation     | Test ticket creation via UI                                                  | Test ticket creation via UI                                            |
| 18   | Backup Strategy          | Configure Windows Task Scheduler for DB backup                               | Setup cron job for DB backup                                           |
| 19   | Monitoring               | Use Event Viewer / IIS logs                                                  | Use syslog / nginx/apache logs                                         |
| 20   | Go-Live                  | Publish internal helpdesk URL                                                | Publish internal helpdesk URL                                          |
``
