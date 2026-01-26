# SpaceDeck Setup Guide for HTB Machine Creators

## Machine Configuration Overview

**Target OS:** Ubuntu 22.04 LTS Server  
**Hostname:** spacedeck  
**Users:**
- `root` (password: randomly generated)
- `astro` (password: `AstroPass2024!`)
- `grafana` (service account)

---

## Installation Steps

### 1. Install Ubuntu 22.04 Server
```bash
# Standard installation, no special packages yet
# Set hostname to 'spacedeck'
sudo hostnamectl set-hostname spacedeck
```

### 2. Install Grafana 11.2.0 (Vulnerable Version)
```bash
# Add Grafana GPG key
wget -q -O - https://apt.grafana.com/gpg.key | sudo apt-key add -

# Add Grafana repository
echo "deb https://apt.grafana.com stable main" | sudo tee /etc/apt/sources.list.d/grafana.list

# Install specific version
sudo apt update
sudo apt install grafana=11.2.0 -y

# Enable and start service
sudo systemctl enable grafana-server
sudo systemctl start grafana-server
```

### 3. Configure Grafana
```bash
# Edit configuration file
sudo nano /etc/grafana/grafana.ini

# Add/modify these sections:
```

**Important config sections:**
```ini
[database]
type = postgres
host = localhost:5432
name = satellite_db
user = astro
password = AstroPass2024!

[security]
admin_user = admin
admin_password = admin
allow_embedding = true
```

**Reset admin password to "admin":**
```bash
sudo grafana-cli admin reset-admin-password admin
sudo systemctl restart grafana-server
```

### 4. Install PostgreSQL (for realism)
```bash
sudo apt install postgresql postgresql-contrib -y
sudo -u postgres psql -c "CREATE DATABASE satellite_db;"
sudo -u postgres psql -c "CREATE USER astro WITH PASSWORD 'AstroPass2024!';"
sudo -u postgres psql -c "GRANT ALL PRIVILEGES ON DATABASE satellite_db TO astro;"
```

### 5. Create User Accounts
```bash
# Create astro user
sudo useradd -m -s /bin/bash astro
echo "astro:AstroPass2024!" | sudo chpasswd

# Create home directory structure
sudo -u astro mkdir -p /home/astro/{.ssh,.config}
```

### 6. Install Nginx for Web Server
```bash
sudo apt install nginx -y

# Create web root
sudo mkdir -p /var/www/spacedeck
sudo chown -R www-data:www-data /var/www/spacedeck

# Copy landing page files
sudo cp /tmp/SpaceDeck_WebFiles/* /var/www/spacedeck/
```

**Nginx Configuration** (`/etc/nginx/sites-available/spacedeck`):
```nginx
server {
    listen 80 default_server;
    server_name _;

    root /var/www/spacedeck;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    location /grafana/ {
        proxy_pass http://localhost:3000/;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

**Enable site:**
```bash
sudo ln -s /etc/nginx/sites-available/spacedeck /etc/nginx/sites-enabled/
sudo rm /etc/nginx/sites-enabled/default
sudo systemctl restart nginx
```

### 7. Configure Sudo for PrivEsc
```bash
sudo visudo

# Add this line:
astro ALL=(ALL) NOPASSWD: /usr/bin/systemctl restart grafana-server
```

### 8. Place Flags
```bash
# User flag
sudo -u astro bash -c 'echo "HTB{gr4f4n4_sql_3xpr3ss10ns_ar3_d4ng3r0us}" > /home/astro/user.txt'
sudo chmod 600 /home/astro/user.txt
sudo chown astro:astro /home/astro/user.txt

# Root flag
sudo bash -c 'echo "HTB{s3rv1c3_wr1t3_pr1v1l3g3s_pwn3d}" > /root/root.txt'
sudo chmod 600 /root/root.txt
```

### 9. Configure SSH
```bash
sudo nano /etc/ssh/sshd_config

# Modify these settings:
PermitRootLogin no
PasswordAuthentication yes
PubkeyAuthentication yes

sudo systemctl restart sshd
```

### 10. Final Hardening
```bash
# Disable unnecessary services
sudo systemctl disable cups bluetooth

# Update firewall rules (if using UFW)
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 3000/tcp
sudo ufw enable

# Remove bash history for clean slate
history -c
sudo -u astro bash -c 'history -c'
```

---

## Testing Checklist

### Before Deployment:
- [ ] Port 80 shows SpaceDeck landing page
- [ ] Port 3000 shows Grafana login
- [ ] Admin login works with `admin:admin`
- [ ] HTML source contains the TODO comment hint
- [ ] Exploitation script successfully triggers RCE
- [ ] `/var/lib/grafana/grafana.db` contains password
- [ ] `/etc/grafana/grafana.ini` contains password
- [ ] `su astro` works with `AstroPass2024!`
- [ ] `sudo -l` shows systemctl permission
- [ ] Service override leads to root shell
- [ ] Both flags are readable only by correct users

---

## Troubleshooting

### Grafana won't start:
```bash
sudo journalctl -u grafana-server -n 50
sudo systemctl status grafana-server
```

### Can't login to Grafana:
```bash
sudo grafana-cli admin reset-admin-password admin
sudo systemctl restart grafana-server
```

### Exploit not working:
- Verify Grafana version is exactly 11.2.0
- Check if SQL Expressions plugin is enabled
- Ensure firewall isn't blocking reverse shell

---

## Files to Include in Submission

1. `SpaceDeck_MachineSpec.md` - Full machine documentation
2. `SpaceDeck_WebFiles/` - Landing page (HTML/CSS)
3. `exploit.py` - Automated exploitation script
4. `setup_guide.md` - This file
5. Screenshots/walkthrough video (optional but recommended)

---

## HTB Submission Notes

**Difficulty Justification:**
- CVE-based with public POC (Easy)
- 2-3 steps (Recon → RCE → PrivEsc)
- No rabbit holes (clear hints)
- Basic scripting only
- Teaches real-world Grafana security

**Unique Selling Points:**
- 2024 CVE (fresh content)
- Sci-fi theme (memorable)
- Realistic scenario (DevOps monitoring)
