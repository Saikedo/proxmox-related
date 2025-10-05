# 🖥️ Proxmox Server Notes

A quick reference of all containers and virtual machines currently running on the Proxmox host.

---

## 🗂️ Overview

| Name | IP Address | Domains | Ports |
|------|-------------|----------|--------|
| **media** | [192.168.68.53](http://192.168.68.53) | — | — |
| **entertainment** | [192.168.68.56](http://192.168.68.56) | [jellyfin.saik22.com](https://jellyfin.saik22.com)<br>[prowlarr.saik22.com](http://prowlarr.saik22.com)<br>[radarr.saik22.com](http://radarr.saik22.com)<br>[sonarr.saik22.com](http://sonarr.saik22.com)<br>[torrent1.saik22.com](http://torrent1.saik22.com)<br>[torrent2.saik22.com](http://torrent2.saik22.com) | [8096](https://jellyfin.saik22.com) *(Jellyfin)*<br>[9696](http://prowlarr.saik22.com) *(Prowlarr)*<br>[7878](http://radarr.saik22.com) *(Radarr)*<br>[8989](http://sonarr.saik22.com) *(Sonarr)*<br>[8080](http://torrent1.saik22.com) *(Torrent #1)*<br>[6789](http://torrent2.saik22.com) *(Torrent #2)* |
| **nginx** | [192.168.68.78](http://192.168.68.78) | — | [81](http://192.168.68.78:81) *(Proxy Manager)* |
| **maxim** | [192.168.68.51](http://192.168.68.51) | [maxim.saik22.com](https://maxim.saik22.com)<br>[minio.maxim.saik22.com](https://minio.maxim.saik22.com) | [3000](https://maxim.saik22.com) *(Next.js)*<br>[4000](http://192.168.68.51:4000) *(Backend)*<br>[9001](https://minio.maxim.saik22.com) *(MinIO)* |
| **dash-and-monitors** | [192.168.68.72](http://192.168.68.72) | — | [7575](http://192.168.68.72:7575) *(Hommar)* |
| **portainer** | [192.168.68.64](https://192.168.68.64:9443) | [portainer.saik22.com](https://portainer.saik22.com) | [9443](https://192.168.68.64:9443) *(Admin Panel)* |

---

## 📦 Details

### 🎬 entertainment
- **IP:** [192.168.68.56](http://192.168.68.56)
- **Domains:**
  - [jellyfin.saik22.com](https://jellyfin.saik22.com) → Jellyfin  
  - [prowlarr.saik22.com](http://prowlarr.saik22.com) → Prowlarr  
  - [radarr.saik22.com](http://radarr.saik22.com) → Radarr  
  - [sonarr.saik22.com](http://sonarr.saik22.com) → Sonarr  
  - [torrent1.saik22.com](http://torrent1.saik22.com) → Torrent Client 1  
  - [torrent2.saik22.com](http://torrent2.saik22.com) → Torrent Client 2  
- **Ports:**
  - [8096](https://jellyfin.saik22.com) → **Jellyfin Web UI**  
  - [9696](http://prowlarr.saik22.com) → **Prowlarr Indexer Manager**  
  - [7878](http://radarr.saik22.com) → **Radarr (Movies)**  
  - [8989](http://sonarr.saik22.com) → **Sonarr (TV Shows)**  
  - [8080](http://torrent1.saik22.com) → **Torrent Client #1**  
  - [6789](http://torrent2.saik22.com) → **Torrent Client #2**  
- **Purpose:** Full media automation stack  
- **Notes:**  
  - Managed via Nginx reverse proxy  
  - Integrates with NZBGet/qBittorrent, Prowlarr, Sonarr, and Radarr for automated fetching  
  - Jellyfin handles local media playback  

---

### 🌐 nginx
- **IP:** [192.168.68.78](http://192.168.68.78)
- **Ports:**
  - [81](http://192.168.68.78:81) → **Nginx Proxy Manager**
- **Purpose:** Reverse proxy for all hosted apps  
- **Notes:** SSL via Let’s Encrypt; routes all `*.saik22.com` domains  

---

### 🚀 maxim
- **IP:** [192.168.68.51](http://192.168.68.51)
- **Domains:**
  - [maxim.saik22.com](https://maxim.saik22.com) → Frontend  
  - [minio.maxim.saik22.com](https://minio.maxim.saik22.com) → MinIO  
- **Ports:**
  - [3000](https://maxim.saik22.com) → **Next.js Frontend**  
  - [4000](http://192.168.68.51:4000) → **Backend API**  
  - [9001](https://minio.maxim.saik22.com) → **MinIO Console**  

---

### 📊 dash-and-monitors
- **IP:** [192.168.68.72](http://192.168.68.72)
- **Ports:**
  - [7575](http://192.168.68.72:7575) → **Hommar Dashboard**

---

### 🧭 portainer
- **IP:** [192.168.68.64](https://192.168.68.64:9443)
- **Domains:**
  - [portainer.saik22.com](https://portainer.saik22.com)
- **Ports:**
  - [9443](https://192.168.68.64:9443) → **Admin Panel**

---

### 🧱 media
- **IP:** [192.168.68.53](http://192.168.68.53)
- **Purpose:** Centralized storage for media and backups  
- **Notes:** Mounted to entertainment and maxim  

---

## 🧰 Useful Commands

```bash
# List containers
pct list

# List VMs (requires QEMU guest agent)
qm list
qm guest exec <vmid> ip a | grep inet
