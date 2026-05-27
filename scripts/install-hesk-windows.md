
# 💻 HESK Automated Installation – Windows Server (IIS)

---

## 📊 Installation Steps (Including Downloads)

| Step | Phase               | Windows (IIS) Action                                | Explanation                            |
|------|--------------------|----------------------------------------------------|----------------------------------------|
| 1    | IIS Install        | Install IIS using PowerShell                       | Enables web server                      |
| 2    | CGI Enable         | Enable CGI feature                                 | Required for PHP execution              |
| 3    | PHP Download       | Download PHP from official Windows PHP website     | Use Thread Safe x64 version             |
| 4    | PHP Version        | Select PHP 8.1 or 8.2                              | Stable and HESK compatible              |
| 5    | PHP Extract        | Extract PHP to C:\PHP                              | Sets runtime directory                  |
| 6    | PHP PATH           | Add PHP to system PATH                             | Makes PHP globally accessible           |
| 7    | IIS PHP Mapping    | Configure Handler Mapping in IIS                   | Links PHP with IIS                      |
| 8    | MariaDB Download   | Download MariaDB from official website             | Database server                         |
| 9    | MariaDB Install    | Install MariaDB using installer                    | Setup DB service                        |
| 10   | DB Start           | Start MariaDB/MySQL service                        | Activates database                      |
| 11   | DB Setup           | Create database and user using MySQL CLI           | Prepares HESK database                  |
| 12   | HESK Download      | Download HESK from official website                | Helpdesk application                    |
| 13   | HESK Extract       | Extract to C:\inetpub\wwwroot\helpdesk             | Deploy application                      |
| 14   | File Copy          | Copy files if required                             | Ensures correct deployment              |
| 15   | Permissions        | Set IIS permissions                                | Required for access                     |
| 16   | IIS Restart        | Restart IIS                                        | Apply changes                           |
| 17   | Run Installer      | Open /helpdesk/install in browser                  | Start HESK setup                        |
| 18   | Configure App      | Enter DB credentials and admin                     | Final configuration                     |
| 19   | Remove Installer   | Delete install folder                              | Security cleanup                        |
| 20   | Enable SSL         | Configure HTTPS in IIS                             | Secure system                           |
| 21   | Backup Setup       | Configure DB backup                                | Data protection                         |
| 22   | Testing            | Create test ticket                                 | Validate working                        |
| 23   | Go-Live           | Publish URL                                        | Production deployment                   |

---


---

## 📌 Download Reference Summary

| Component | Download Location | Recommended Version | Notes |
|----------|------------------|--------------------|------|
| PHP | https://windows.php.net/download/ | 8.1 / 8.2 | Use Thread Safe ZIP |
| MariaDB | https://mariadb.org/download/ | Latest Stable | Production-ready DB |
| HESK | https://www.hesk.com/download/ | Latest | Lightweight Helpdesk |

---

## ⚠️ Important Compatibility Notes

- ✅ Use **PHP Thread Safe (TS)** for IIS  
- ✅ Enable required PHP extensions:
  - mysqli  
  - gd  
  - curl  
  - mbstring  

- ✅ Do NOT use:
  - Non-thread-safe PHP with IIS (unless FCGI properly configured)

---

## ✅ Optional: Automated Download (PowerShell)

> ⚠️ Use with caution in production

```powershell
# Download PHP
Invoke-WebRequest -Uri "https://windows.php.net/downloads/releases/php-8.2.0-Win32-vs16-x64.zip" -OutFile "C:\Temp\php.zip"

# Extract PHP
Expand-Archive -Path "C:\Temp\php.zip" -DestinationPath "C:\PHP"

# Download HESK
Invoke-WebRequest -Uri "https://www.hesk.com/files/hesk.zip" -OutFile "C:\Temp\hesk.zip"

# Extract HESK
Expand-Archive -Path "C:\Temp\hesk.zip" -DestinationPath "C:\inetpub\wwwroot\helpdesk"
