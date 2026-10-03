# 🛡️ Enterprise Web Application Firewall (WAF)

A hands-on cybersecurity project demonstrating the deployment and testing of **ModSecurity WAF** with **OWASP Core Rule Set (CRS)** on an **Nginx web server** running on Ubuntu Server.

## 🏗️ Architecture

```text
Kali Linux (10.0.2.4)
        │
        │ Crafted HTTP Requests
        ▼
Ubuntu Server (10.0.2.15)
        │
      Nginx
        │
  ModSecurity WAF
        │
    OWASP CRS
        │
   ┌────┴────┐
   ▼         ▼
 ALLOW      BLOCK
  200        403
```

## 🧪 Attack Testing

| Attack            | Payload                     | Result   | CRS Rule |
| ----------------- | --------------------------- | -------- | -------- |
| ✅ Legitimate      | `?query=tea`                | `200 OK` | —        |
| 🔴 SQL Injection  | `' OR '1'='1`               | `403`    | `942100` |
| 🔴 XSS            | `<script>alert(1)</script>` | `403`    | `941110` |
| 🔴 Path Traversal | `../../../../etc/passwd`    | `403`    | `930110` |

## ⚙️ Implementation

* Enabled ModSecurity active enforcement: `SecRuleEngine On`
* Integrated **OWASP Core Rule Set (CRS)**
* Used **Kali Linux + curl** for attack simulation
* Analyzed ModSecurity audit logs
* Configured **Nginx** as the web server

## 🔐 Security Concepts

* Web Application Firewall (WAF)
* SQL Injection & XSS detection
* Path Traversal protection
* HTTP request inspection
* OWASP CRS rule detection
* Security log analysis
* WAF rule tuning and false-positive handling

## 🛠️ Technologies

`Ubuntu Server` · `Kali Linux` · `Nginx` · `ModSecurity v3` · `OWASP CRS` · `curl`
