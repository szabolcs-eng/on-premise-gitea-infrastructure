# Secure On-Premise Git Infrastructure & Web Environment

This project demonstrates the design and implementation of a professional, local (on-premise) development infrastructure for a startup. It includes a secure version control system (Gitea), a local DNS service, and a web server with reverse proxy capabilities.

## 🚀 Key Features & Infrastructure
- **Server OS:** Ubuntu Server 24.04 LTS (Dual-server architecture)
- **Client OS:** Windows 11 Pro with BitLocker encryption
- **Version Control:** Gitea (Self-hosted)
- **Web Server:** Nginx as a Reverse Proxy
- **Local DNS:** Dnsmasq for internal name resolution
- **Security:** SSH Ed25519 key-based authentication, UFW firewall hardening

## 🛠️ System Architecture
The system is divided into two main segments:
1. **Server LAN (192.168.20.0/24):** Hosts the Web/DNS Server and the Gitea/Database Server.
2. **Workgroup LAN (192.168.10.0/24):** For development clients and management.

## 🔧 Critical Configurations
- **Reverse Proxy:** Nginx redirects port 80 traffic to Gitea's internal port 3000.
- **SSH Hardening:** Gitea's built-in SSH server is configured on port 2222 to separate Git operations from administrative access.
- **Data Integrity:** MySQL database backend for high-performance repository management.

## 💡 Troubleshooting (The "Lesson Learned" section)
One of the key achievements in this project was identifying and resolving several network bottlenecks:

*   **Issue:** Internal DNS timeout when accessing `gitea.hightech.local`.
    *   **Fix:** Diagnosed that the DNS was pointing directly to the Gitea server instead of the Nginx proxy. Corrected the Dnsmasq records to point to the Web Server (192.168.20.10).
*   **Issue:** SSH "Connection Refused" on port 2222.
    *   **Fix:** Identified that the internal Gitea SSH server was disabled by default. Modified `app.ini` to enable `START_SSH_SERVER = true` and ensured port 2222 was listening.

## 📂 Repository Structure
- `/nginx`: Nginx virtual host configurations.
- `/dns`: Dnsmasq internal zone settings.
- `/gitea`: Core Gitea configuration snippets (app.ini).
- `/html`: The "High-Tech Solutions" landing page code.
