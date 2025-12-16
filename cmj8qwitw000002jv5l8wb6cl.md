---
title: "🚀 Nginx Configuration for Node.js Apps (PM2 + Ubuntu)"
seoTitle: "Nginx Configuration for Node.js Apps (PM2 + Ubuntu)"
seoDescription: "personal reference guide for configuring Nginx as a reverse proxy in front of a Node.js application managed by PM2 on Ubuntu."
datePublished: Tue Dec 16 2025 15:36:31 GMT+0000 (Coordinated Universal Time)
cuid: cmj8qwitw000002jv5l8wb6cl
slug: nginx-configuration-for-nodejs-apps-pm2-ubuntu
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1765899370552/6ceae590-0a42-4ec8-98df-735630952149.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1765899374956/f6a041db-66ec-40b4-bef8-2710e627296b.png
tags: server, nginx, nodejs, pm2, production

---

This article is a **personal reference guide** for configuring **Nginx as a reverse proxy** in front of a **Node.js application managed by PM2** on Ubuntu.

It focuses on **what actually matters in production**.

---

## 🧠 Why Nginx?

Nginx sits between the internet and your Node app.

**Responsibilities:**

* Accept public traffic (port 80 / 443)
    
* Forward requests to Node ([localhost](http://localhost))
    
* Handle large payloads (PDFs, uploads)
    
* Enable HTTPS
    
* Improve security & stability
    

Node **should not** be directly exposed to the internet.

---

## 📦 Install Nginx

```bash
sudo apt update
sudo apt install -y nginx
```

Verify:

```bash
systemctl status nginx
```

Test:

```bash
curl http://localhost
```

---

## 🗂 Nginx Directory Structure (Important)

```text
/etc/nginx/
 ├── nginx.conf
 ├── sites-available/
 │    └── my-app
 └── sites-enabled/
      └── my-app -> ../sites-available/my-app
```

**Rule:**

* Write configs in `sites-available`
    
* Enable them using a symlink in `sites-enabled`
    

---

## 🔎 Check Existing Configurations

```bash
ls /etc/nginx/sites-available
ls /etc/nginx/sites-enabled
```

View loaded configs:

```bash
sudo nginx -T
```

---

## ⚙️ Basic Reverse Proxy Configuration

Create a config file:

```bash
sudo nano /etc/nginx/sites-available/my-app
```

```nginx
server {
    listen 80;
    server_name YOUR_DOMAIN_OR_IP;

    location / {
        proxy_pass http://127.0.0.1:3000;
        proxy_http_version 1.1;

        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;

        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        proxy_cache_bypass $http_upgrade;
    }
}
```

---

## 🔗 Enable the Site

```bash
sudo ln -s /etc/nginx/sites-available/my-app \
           /etc/nginx/sites-enabled/
```

Disable default site (recommended):

```bash
sudo rm /etc/nginx/sites-enabled/default
```

---

## 🧪 Validate & Reload

```bash
sudo nginx -t
sudo systemctl reload nginx
```

---

## 🧠 Node.js Best Practice

Bind Node **only to** [**localhost**](http://localhost):

```js
app.listen(3000, "127.0.0.1");
```

This prevents direct external access.

---

## 📄 Handling Large Requests (PDFs, Uploads)

Add inside `server {}`:

```nginx
client_max_body_size 50M;

proxy_connect_timeout 300;
proxy_send_timeout 300;
proxy_read_timeout 300;
send_timeout 300;
```

This avoids timeout failures for long-running tasks.

---

## 📊 Logs & Debugging

### Nginx

```bash
sudo tail -f /var/log/nginx/access.log
sudo tail -f /var/log/nginx/error.log
```

### Node (PM2)

```bash
pm2 logs my-app
```

---

## 🔐 Enable HTTPS (Let’s Encrypt)

```bash
sudo apt install -y certbot python3-certbot-nginx
sudo certbot --nginx -d yourdomain.com
```

Auto-renew test:

```bash
sudo certbot renew --dry-run
```

---

## 🧠 Production Checklist

✔ Node running via PM2  
✔ App bound to [localhost](http://localhost)  
✔ Nginx reverse proxy enabled  
✔ Large payload support  
✔ HTTPS enabled  
✔ Auto-restart on reboot

---

## 🧯 Common Mistakes

* ❌ Running Node on port 80
    
* ❌ Exposing Node publicly
    
* ❌ Installing OS packages via npm
    
* ❌ Forgetting timeouts for long jobs
    
* ❌ Editing `nginx.conf` directly
    

---

## 🏁 Final Thoughts

Nginx + PM2 is a **battle-tested setup** for Node.js apps.

Once configured properly:

* Deployments are safer
    
* Restarts are painless
    
* Scaling is easier
    
* Debugging is predictable
    

This setup has saved me **hours during production incidents**.

---