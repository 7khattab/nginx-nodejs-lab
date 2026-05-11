````markdown
# 🚀 NGINX Reverse Proxy + Node.js Production-Like Lab

A hands-on DevOps lab focused on building a production-style web architecture using **NGINX** and a real **Node.js application**.

This project demonstrates how NGINX works as a:
- Reverse Proxy
- SSL/TLS termination layer
- HTTP → HTTPS redirect gateway

The goal of this repository is not only to learn NGINX basics, but to gradually evolve this lab into a complete DevOps project including:
- Docker
- Kubernetes
- Monitoring
- CI/CD
- Load Balancing
- Infrastructure Automation

---

# 📁 Project Structure

```bash
nginx-nodejs-lab/
│
├── app/              # Node.js application
├── nginx/            # NGINX configurations
├── docs/             # Documentation and notes
├── result_images/    # Screenshots and outputs
├── README.md
└── LICENSE
````

---

# 🧠 Architecture

```text
Client
   ↓
HTTP Request
   ↓
NGINX :80
   ↓
301 Redirect
   ↓
HTTPS :443
   ↓
Reverse Proxy
   ↓
Node.js Application :5006
```

---

# ⚙️ Technologies Used

* NGINX
* Node.js
* OpenSSL
* Linux
* Git & GitHub

---

# ✨ Features Implemented

## ✅ Reverse Proxy

NGINX forwards incoming client requests to the backend Node.js application.

## ✅ SSL/TLS Encryption

Self-signed SSL certificates were created using OpenSSL to secure traffic over HTTPS.

## ✅ HTTP → HTTPS Redirection

All HTTP requests are automatically redirected to HTTPS.

## ✅ Real Node.js Application

Instead of a simple demo server, a real Node.js application was used.

## ✅ Domain Simulation

Local domain mapping using `/etc/hosts`.

---

# 🔧 NGINX Configuration

```nginx
server {
    listen 80;
    server_name node_app.com;

    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name node_app.com;

    ssl_certificate     /etc/nginx/ssl/certificate.crt;
    ssl_certificate_key /etc/nginx/ssl/private.key;

    location / {
        proxy_pass http://127.0.0.1:5006;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto https;
    }
}
```

---

# 🧪 Testing

## Test HTTP Redirect

```bash
curl http://node_app.com
```

Expected:

```text
301 Moved Permanently
```

---

## Test HTTPS

```bash
curl -k https://node_app.com
```

Expected:

```text
Node.js application response
```

---

# 🔐 SSL Certificate Generation

```bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
-keyout key.pem \
-out cert.pem
```

---

# 🚀 Future Improvements

This repository will continue evolving into a complete DevOps project.

Upcoming updates include:

* [ ] Dockerizing the application
* [ ] Docker Compose setup
* [ ] NGINX Load Balancing
* [ ] Kubernetes Deployment
* [ ] Ingress Controller
* [ ] Prometheus Monitoring
* [ ] Grafana Dashboards
* [ ] CI/CD with GitHub Actions
* [ ] Infrastructure as Code
* [ ] Security Hardening
* [ ] Multi-service Architecture

---

# 🎯 Learning Objectives

This lab was built to practice:

* NGINX fundamentals
* Reverse proxy concepts
* SSL/TLS basics
* Production-style architecture
* Linux networking concepts
* Real-world DevOps workflows

---

# 📌 Notes

This is an educational and continuously evolving project.

More production-grade improvements and DevOps practices will be added over time.

---

# 👨‍💻 Author

Mohamed Khattab

```
```

