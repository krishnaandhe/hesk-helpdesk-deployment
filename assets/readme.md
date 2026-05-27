## 🧭 Architecture Explanation

The HESK Helpdesk system follows a standard web-based architecture:

1. Users access via web browser or email
2. Traffic passes through firewall/security layer
3. IIS Web Server processes HTTP requests
4. PHP engine runs HESK application logic
5. HESK interacts with:
   - Database (MySQL / MariaDB) → stores tickets, users, logs
   - File Storage → attachments & system data
   - SMTP Server → email notifications

This ensures centralized ticketing, secure access, and scalable operations.
