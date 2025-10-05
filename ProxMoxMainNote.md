# 🖥️ Proxmox Server Notes

A quick reference of all containers and virtual machines currently running on the Proxmox host.

---

## 🗂️ Overview

| Name | IP Address | Domains | Ports |
|------|-------------|----------|--------|
| **media** | [192.168.68.53](http://192.168.68.53) | — | — |
| **entertainment** | [192.168.68.56](http://192.168.68.56) | — | [8096](http://192.168.68.56:8096) *(Jellyfin)* |
| **nginx** | [192.168.68.78](http://192.168.68.78) | — | [81](http://192.168.68.78:81) *(Proxy Manager)* |
| **maxim** | [192.168.68.51](http://192.168.68.51) | [maxim.saik22.com](https://maxim.saik22.com)<br>[minio.maxim.saik22.com](https://minio.maxim.saik22.com) | [3000](https://maxim.saik22.com) *(Next.js)*<br>[4000](http://192.168.68.51:4000) *(Backend)*<br>[9001](https://minio.maxim.saik22.com) *(MinIO)* |
| **dash-and-monitors** | [192.168.68.72](http://192.168.68.72) | — | [7575](http://192.168.68.72:7575) *(Hommar)* |
| **portainer** | [192.168.68.64](https://192.168.68.64:9443) | — | [9443](https://192.168.68.64:9443) *(Admin Panel)* |

---

## 📦 Details

### 🧱 media
- **IP:** [192.168.68.53](http://192.168.68.53)
- **Purpose:** Centralized storage for media and backups  
- **Notes:** Mounted to entertainment and maxim  

---

### 🎬 entertainment
- **IP:** [192.168.68.56](http://192.168.68.56)
- **Ports:**
  - [8096](http://192.168.68.56:8096) → **Jellyfin Web UI**
- **Purpose:** Media streaming and transcoding  
- **Notes:** Hardware transcoding enabled  

---

### 🌐 nginx
- **IP:** [192.168.68.78](http://192.168.68.78)
- **Ports:**
  - [81](http://192.168.68.78:81) → **Proxy Manager Dashboard**
- **Purpose:** Reverse proxy for all local and public services  
- **Notes:** Handles SSL & routing (`*.saik22.com`)  

---

### 🚀 maxim
- **IP:** [192.168.68.51](http://192.168.68.51)
- **Domains:**
  - [maxim.saik22.com](https://maxim.saik22.com) → Next.js Frontend  
  - [minio.maxim.saik22.com](https://minio.maxim.saik22.com) → MinIO Storage  
- **Ports:**
  - [3000](https://maxim.saik22.com) → **Next.js Frontend**  
  - [4000](http://192.168.68.51:4000) → **Backend API**  
  - [9001](https://minio.maxim.saik22.com) → **MinIO Console**  
- **Purpose:** Full-stack web platform  
- **Notes:** Managed by nginx; connected to DB and MinIO  

---

### 📊 dash-and-monitors
- **IP:** [192.168.68.72](http://192.168.68.72)
- **Ports:**
  - [7575](http://192.168.68.72:7575) → **Hommar Dashboard**
- **Purpose:** Internal dashboards and monitoring tools  
- **Notes:** Runs on lightweight VM  

---

### 🧭 portainer
- **IP:** [192.168.68.64](https://192.168.68.64:9443)
- **Ports:**
  - [9443](https://192.168.68.64:9443) → **Admin Panel**
- **Purpose:** Centralized Docker management for all nodes  
- **Notes:** Connects to agents on each Docker VM  

---

## 🧰 Useful Commands

```bash
# List containers
pct list

# List VMs (requires QEMU guest agent)
qm list
qm guest exec <vmid> ip a | grep inet
