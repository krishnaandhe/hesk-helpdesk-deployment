# 💻 HESK Automated Installation – Windows Server (IIS)

---

## 📌 Overview

This document provides a **fully automated PowerShell-based deployment** of:

- IIS Web Server
- PHP Runtime
- MySQL Database
- HESK Helpdesk Application

Designed for **enterprise environments** running Windows Server.

---

## ⚙️ Installation Flow (Automated + Explained)

| Step | Phase              | PowerShell / Command                                                                 | Explanation                                                                 |
|------|-------------------|--------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| 1    | IIS Installation  | `Install-WindowsFeature Web-Server -IncludeManagementTools`                         | Installs IIS web server role                                                |
| 2    | CGI Enable        | `Install-WindowsFeature Web-CGI`                                                    | Enables PHP support in IIS                                                  |
| 3    | Create PHP Dir    | `New-Item -Path "C:\PHP" -ItemType Directory`                                       | Creates PHP installation directory                                          |
| 4    | Extract PHP       | Manual download → extract to `C:\PHP`                                               | PHP binaries required to run HESK                                           |
| 5    | Set Environment   | `setx PATH "$($env:PATH);C:\PHP" /M`                                                | Adds PHP to system PATH                                                     |
| 6    | Install MySQL     | `winget install MySQL.MySQLServer`                                                  | Installs MySQL database                                                     |
| 7    | Start MySQL       | `net start MySQL`                                                                   | Starts MySQL service                                                        |
| 8    | Create DB         | `mysql -u root -p` (manual SQL execution)                                           | Create HESK database and user                                               |
| 9    | Create Web Dir    | `New-Item -Path "C:\inetpub\wwwroot\helpdesk" -ItemType Directory`                  | Creates application directory                                               |
| 10   | Copy HESK Files   | `xcopy D:\hesk C:\inetpub\wwwroot\helpdesk /E /I`                                   | Deploys HESK application                                                    |
| 11   | Set Permissions   | `icacls C:\inetpub\wwwroot\helpdesk /grant IIS_IUSRS:(OI)(CI)F /T`                 | Grants IIS access to files                                                  |
| 12   | IIS Restart       | `iisreset`                                                                        | Applies IIS configuration                                                   |
| 13   | Access Installer  | `http://localhost/helpdesk/install`                                                | Launches web-based HESK installer                                           |
| 14   | Remove Installer  | `Remove-Item "C:\inetpub\wwwroot\helpdesk\install" -Recurse`                       | Removes installation directory (security)                                   |
| 15   | Backup Setup      | `mysqldump -u root -p hesk_db > C:\backup\hesk.sql`                                 | Creates database backup                                                     |
| 16   | Final Validation  | Open browser → Create test ticket                                                  | Ensures system is working                                                   |

---

## 🚀 Full Automation Script (PowerShell)

> ⚠️ Run PowerShell as Administrator

```powershell
# ===============================
# HESK AUTO INSTALL SCRIPT (WINDOWS)
# ===============================

Write-Host "Starting HESK Deployment..." -ForegroundColor Green

# 1. Install IIS
Install-WindowsFeature Web-Server -IncludeManagementTools
Install-WindowsFeature Web-CGI

# 2. Create PHP Directory
New-Item -Path "C:\PHP" -ItemType Directory -Force

Write-Host "Please download PHP manually and extract to C:\PHP"
Pause

# 3. Set PATH
setx PATH "$($env:PATH);C:\PHP" /M

# 4. Install MySQL
winget install -e --id MySQL.MySQLServer

Start-Sleep -Seconds 20

# 5. Start MySQL
net start MySQL

Write-Host "Please configure MySQL Root Password and create database"
Pause

# 6. Create Web Directory
New-Item -Path "C:\inetpub\wwwroot\helpdesk" -ItemType Directory -Force

Write-Host "Copy HESK files into C:\inetpub\wwwroot\helpdesk"
Pause

# 7. Set Permissions
icacls "C:\inetpub\wwwroot\helpdesk" /grant IIS_IUSRS:(OI)(CI)F /T

# 8. Restart IIS
iisreset

Write-Host "Open browser and complete installation:"
Write-Host "http://localhost/helpdesk/install"

Pause

# 9. Clean Install Folder
Remove-Item "C:\inetpub\wwwroot\helpdesk\install" -Recurse -Force

Write-Host "HESK Deployment Completed Successfully!" -ForegroundColor Green
