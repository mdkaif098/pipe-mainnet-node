# ⚡️ Pipe Mainnet Node Setup Guide

A quick and clean guide to get your **PipeCDN (Pipe Network) node** online and ready for **Mainnet**.

---

## 🧩 1. Requirements

**Supported OS:**  
- Ubuntu **24.04+** or Debian **11+**

**Open TCP Ports:**  
- `80` and `443`

**Hardware:**  
- Minimum **20 GB** free space  
- SSD/NVMe strongly recommended for cache performance

---

## ⚙️ 2. Installation

### 🧱 Step 1 — Create installation directory
```bash
cd /opt
mkdir pipe && cd pipe
```
### ⬇️ Step 2 — Download the latest binary
```bash
curl -L https://pipe.network/p1-cdn/releases/latest/download/pop -o pop
chmod +x pop
```

## 🌐 3. Open TCP Ports

```bash
sudo ufw allow 22
sudo ufw allow 443/tcp
sudo ufw allow 80/tcp
sudo ufw enable
sudo ufw status verbose
```

## ⚙️ 4. Configuration

### Create a new file named .env inside /opt/pipe:
```bash
nano /opt/pipe/.env
```
### Paste the following and edit as per your setup:
```bash
# Wallet for earnings
NODE_SOLANA_PUBLIC_KEY=your_solana_wallet_address

# Node identity
NODE_NAME=my-pop-node
NODE_EMAIL="operator@example.com"
NODE_LOCATION="San Francisco, USA"

# Cache configuration
MEMORY_CACHE_SIZE_MB=512
DISK_CACHE_SIZE_GB=100
DISK_CACHE_PATH=./cache

# Network ports
HTTP_PORT=80
HTTPS_PORT=443

# Home network auto port forwarding (disable on VPS/servers)
UPNP_ENABLED=false
```
📝 **Edit these values before saving:**
- `NODE_SOLANA_PUBLIC_KEY` → Enter your **Solana wallet address** for earnings  
- `NODE_NAME` → Enter **any name** for your node (e.g., `pipe-node-01`)  
- `NODE_EMAIL` → Enter your **own Gmail**  
- `NODE_LOCATION` → Enter your **VPS or server location** (e.g., `Frankfurt, Germany`)

💾 **To save and exit the file:**
- Press CTRL + O → then hit Enter (to save)
- Press CTRL + X (to exit Nano editor)

## 🚀 5. Run the Node

### Create a systemd service file:
```bash
sudo nano /etc/systemd/system/pipe.service
```
### Paste the following:
```bash
[Unit]
Description=Pipe Network POP Node
After=network-online.target
Wants=network-online.target

[Service]
WorkingDirectory=/opt/pipe
ExecStart=/bin/bash -c 'source /opt/pipe/.env && /opt/pipe/pop'
Restart=always
RestartSec=5
StandardOutput=journal
StandardError=journal
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
```
### Enable and start the service:
```bash
sudo systemctl daemon-reload
sudo systemctl enable pipe
sudo systemctl start pipe
sudo journalctl -u pipe -f
```

## 📊 6. Monitoring Your Node

### Check your node status and earnings anytime:
```bash
cd /opt/pipe
./pop status
./pop earnings
```

## 🧠 Notes

### To stop the node:
```bash
sudo systemctl stop pipe
```
### To restart after config updates:
```bash
sudo systemctl restart pipe
```

---

## 📢 Community & Support

- Stay connected and get updates:

💬 Telegram: [kind_cr](https://t.me/kind_cr)

🐦 X (Twitter): [@Mohamma34525340](https://x.com/Mohamma34525340) & [@armaanbhat201](https://x.com/armaanbhat201)

▶️ YouTube: [KindCrypto](https://www.youtube.com/@KindCrypto)
