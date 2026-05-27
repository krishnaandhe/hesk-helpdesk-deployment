# 💻 HESK Automated Installation – Windows Server (IIS)

---

## 📊 Installation Steps (Including Downloads)

| Step | Phase                | Windows (IIS) Action                                                     | Explanation                                      |
|------|---------------------|-------------------------------------------------------------------------|--------------------------------------------------|
| 1    | IIS Install         | Install IIS using PowerShell                                             | Enables web server                               |
| 2    | CGI Enable          | Enable CGI feature                                                       | Required for PHP execution                       |

| 3    | PHP Download        | Download PHP from Windows PHP official site                              | Use latest Thread Safe x64 version               |
| 4    | PHP Version         | Select PHP 8.1 or 8.2                                                    | Stable and HESK compatible                       |
| 5    | PHP Extract         | Extract PHP to C:\PHP                                                    | Sets runtime directory                           |
| 6    | PHP PATH            | Add PHP to system PATH                                                   | Makes PHP globally accessible                    |
| 7    | IIS PHP Mapping     | Configure Handler Mapping in IIS                                         | Links PHP with IIS                               |

| 8    | MariaDB Download    | Download MariaDB from official website                                   | Database server                                  |
| 9    | MariaDB Install     | Install using installer                                                  | Setup DB service                                 |
| 10   | DB Start            | Start MariaDB/MySQL service                                              | Activates DB                                     |
| 11   | DB Setup            | Create DB and user using MySQL CLI                                       | Prepares HESK database                           |

| 12   | HESK Download       | Download HESK from official website                                      | Helpdesk application                             |
| 13   | HESK Extract        | Extract to C:\inetpub\wwwroot\helpdesk                                   | Deploy application                               |

| 14   | File Copy           | Copy files if required                                                   | Ensures correct deployment                       |
| 15   | Permissions         | Grant IIS permissions                                                    | Required for access                              |
| 16   | IIS Restart         | Restart IIS                                                              | Apply changes                                    |

| 17   | Run Installer       | Open /helpdesk/install in browser                                        | Start HESK setup                                 |
| 18   | Configure App       | Enter DB credentials & admin user                                        | Final configuration                              |
| 19   | Remove Installer    | Delete install folder                                                    | Security cleanup                                 |

| 20   | Enable SSL          | Configure HTTPS in IIS                                                   | Secure platform                                  |
| 21   | Backup Setup        | Configure database backup                                                | Data safety                                      |
| 22   | Testing             | Create test ticket                                                       | Validate system                                  |
| 23   | Go-Live            | Publish URL internally                                                   | Production deployment                            |

---

## 📌 Download Sources

- PHP → Windows PHP official download site  
- MariaDB → MariaDB official website  
- HESK → HESK official website  

---

## ⚠️ Important Notes

- Always use **Thread Safe PHP for IIS**
- Validate versions before deployment
- Prefer manual verified download in production environments

---
``
