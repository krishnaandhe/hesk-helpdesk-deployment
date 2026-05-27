# 💻 HESK Automated Installation – Windows Server (IIS)

---

## 📊 Installation Steps (Including Downloads)

| Step | Phase                     | PowerShell / Action                                                                 | Explanation                                                                 |
|------|--------------------------|-------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| 1    | IIS Installation         | `Install-WindowsFeature Web-Server -IncludeManagementTools`                        | Installs IIS Web Server                                                     |
| 2    | Enable CGI               | `Install-WindowsFeature Web-CGI`                                                   | Required for PHP execution                                                   |

| 3    | Download PHP             | Visit:<br>https://windows.php.net/download/                                         | Download latest **Thread Safe (TS) x64 ZIP** version                        |
| 4    | PHP Version Selection    | Recommended:<br>PHP 8.1 / 8.2                                                       | Stable and compatible with HESK                                             |
| 5    | Extract PHP              | Extract to:<br>`C:\PHP`                                                            | PHP runtime location                                                        |
| 6    | Configure PATH           | `setx PATH "$($env:PATH);C:\PHP" /M`                                               | Makes PHP globally accessible                                               |
| 7    | PHP IIS Mapping          | Manual in IIS Manager → Handler Mapping                                            | Links PHP with IIS                                                          |

| 8    | Download MariaDB         | Visit:<br>https://mariadb.org/download/                                            | Download latest stable version                                              |
| 9    | Install MariaDB          | Run installer manually OR use winget                                               | Database server installation                                                |
| 10   | Start DB Service         | `net start MySQL` (or MariaDB service)                                             | Starts database service                                                     |

| 11   | Database Setup           | `mysql -u root -p`                                                                 | Enter DB shell                                                              |
| 12   | Create DB & User        | SQL:<br>`CREATE DATABASE hesk_db;`<br>`CREATE USER...;`                            | Prepare HESK database                                                       |

| 13   | Download HESK            | Visit:<br>https://www.hesk.com/download/                                           | Download latest HESK ZIP package                                            |
| 14   | Extract HESK             | Extract to:<br>`C:\inetpub\wwwroot\helpdesk`                                       | Application deployment location                                             |

| 15   | File Copy (Optional)     | `xcopy D:\hesk C:\inetpub\wwwroot\helpdesk /E /I`                                  | Automates file deployment                                                   |
| 16   | Set Permissions          | `icacls helpdesk /grant IIS_IUSRS:(OI)(CI)F /T`                                   | Enables IIS access                                                          |

| 17   | Restart IIS              | `iisreset`                                                                        | Applies configuration                                                       |

| 18   | Run Installer           | Open:<br>`http://localhost/helpdesk/install`                                       | Web installer setup                                                         |
| 19   | Configure App           | Enter DB details + Admin setup                                                    | Final configuration                                                         |
| 20   | Remove Install Folder   | `Remove-Item helpdesk\install -Recurse`                                            | Security cleanup                                                            |

| 21   | Enable SSL              | Configure in IIS (Bindings)                                                       | Secure HTTPS setup                                                          |
| 22   | Backup Setup            | `mysqldump -u root -p hesk_db > C:\backup\hesk.sql`                              | Data backup                                                                 |
| 23   | Final Testing           | Create test ticket                                                               | Validate system                                                             |

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
