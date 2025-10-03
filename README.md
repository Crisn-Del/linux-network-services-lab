# linux-network-services-lab
Configure DNS, SMTP, LDA (IMAP), Web, Database, LDAP, firewall

This project demonstrates how to configure multiple Linux services to work together in a networked environment, including **DNS, Mail (SMTP + LDA), Web Server, Database, and LDAP authentication**.  
All services were configured and tested on CentOS/RHEL-based VMs.

---

## 🎯 Objectives
- Configure **DNS (BIND)** with Master/Slave setup
- Enable **SMTP (Postfix)** and test mail delivery
- Configure **LDA (Dovecot)** for IMAP and mail storage
- Set up **Web Server (Apache + PHP)**
- Install and configure **MariaDB** with Roundcube webmail
- Apply **firewall rules** using `iptables`

---

## 📂 Repository Layout
- `dns/` → BIND configuration files (zones, named.conf)
- `smtp/` → Postfix configuration
- `lda/` → Dovecot & Postfix integration configs
- `web/` → Apache and PHP setup with test pages
- `db/` → SQL scripts for MariaDB and Roundcube
- `firewall/` → iptables service rules
- `scripts/` → automation helpers (setup commands)

---

## 🚀 Setup Steps

### 1️⃣ Firewall and iptables
```bash
systemctl stop firewalld
systemctl disable firewalld
systemctl mask firewalld

yum install iptables-services
systemctl enable iptables
systemctl start iptables
2️⃣ DNS (BIND Master/Slave)
Master → server.cfonseca.ops (192.168.0.10)

Slave → client.cfonseca.ops (192.168.0.20)

Config files:

dns/named.conf

dns/mydb-for-cfonseca-ops

dns/mydb-for-192.168.0

3️⃣ SMTP (Postfix) + LDA (Dovecot)
Install Postfix & Mailx

Configure /etc/postfix/main.cf

Enable Dovecot IMAP + Maildir

Firewall ports: 25 (SMTP), 143 (IMAP), 993 (IMAPS)

4️⃣ Web Server (Apache + PHP)
bash
Copy code
yum install httpd php
systemctl enable httpd
systemctl start httpd
Test page → web/index.php

5️⃣ Database (MariaDB + Roundcube)
Install and start MariaDB

Create DB + User for Roundcube

Configure Apache Roundcube webmail

6️⃣ LDAP Authentication (if required)
Configure client VM:

bash
Copy code
authconfig --enableldap --enableldapauth \
 --ldapserver=ops345.com \
 --ldapbasedn="dc=ops345,dc=com" \
 --enablemkhomedir --update
