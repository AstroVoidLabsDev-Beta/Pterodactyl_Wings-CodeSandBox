# 🚀 Pterodactyl Wings Installation Guide with SSL & Cloudflare Tunnel

This repository provides a simple guide to installing and configuring **Pterodactyl Wings** with SSL certificates and Cloudflare tunneling.  
Follow the steps below carefully to set up your node successfully.

---

## 📋 Steps to Install

### 1. Install Wings
```bash
bash <(curl -s https://pterodactyl-installer.se)
```

### 2. Create Your Wings Node
- Add your node inside the **Pterodactyl Panel**.

### 3. Setup Cloudflare Tunnel
1. Go to [Cloudflare Dashboard](https://dash.cloudflare.com)  
2. Create a tunnel on port `localhost:8080` (use **HTTP** connection).  
3. Copy your tunnel public hostname (example: `wings.example.com`).  
4. Paste this domain in the **FQDN** field of your panel.

### 4. Setup SSL for Localhost
```bash
mkdir -p /etc/certs
cd /etc/certs
openssl req -new -newkey rsa:4096 -days 3650 -nodes -x509 -subj "/C=NA/ST=NA/L=NA/O=NA/CN=Generic SSL Certificate" -keyout privkey.pem -out fullchain.pem
```
📌 *Code credit: How2MCoffic*  

### 5. Edit Wings Configuration
Open the config file:
```bash
nano /etc/pterodactyl/config.yml
```
Update the SSL section:
```yaml
ssl:
   enabled: false
   cert: /etc/certs/fullchain.pem
   key: /etc/certs/privkey.pem
```

### 6. Debug Wings
```bash
wings --debug
```

### 7. Fix Network Errors (if any)
```bash
docker network create --driver bridge --subnet 172.30.0.0/16 pterodactyl_nw
```

### 8. Start Wings Service
```bash
systemctl start wings
```

### 9. Final Node Settings
If your node doesn’t come online:
- Go to: `https://ptero.example.com/admin/nodes/view/2/settings`
- Change **Daemon Port** from `8080` → `443`
- Save changes ✅

---

## 🎉 Success
Your **Pterodactyl Wings** should now be running successfully with SSL enabled!  

---

## 📝 Credits
- Guide: **ITZ_YTANSH**  
- SSL Code Snippet: **How2MCoffic**
- Codes: **HopingBoyz**
