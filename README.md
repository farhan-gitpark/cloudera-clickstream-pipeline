# cloudera-clickstream-pipeline
End-to-end real-time Cloudera Big Data platform project for clickstream processing.











# 🛠️ Cloudera Bare Metal Deployment Using Tarball (Admin Project)

## 📘 Project Overview

This project covers a **complete Cloudera Data Platform (CDP)** deployment on **bare metal (on-premises) Linux servers using tarball installation**, focusing on real-world enterprise setup practices. It's designed to demonstrate deep understanding of **infrastructure provisioning, service configuration, ingestion, security, and administration** — all hands-on.

---

## 🧱 1. Infrastructure & Pre-Installation Setup

### ✅ Performed on All Nodes (Master, Worker, Edge):

- Set hostnames
- Configured `/etc/hosts` for IP-hostname mapping
- Set static IPs and custom DNS
- Disabled SELinux & Transparent Huge Pages
- Enabled NTP (chrony or ntpd)
- Created `cloudera` user for CM operations (optional but recommended)

---

## 📦 2. Install Required Packages

- Java 8 or Java 11
- Tools: `wget`, `curl`, `net-tools`, `vim`, `chrony`
- Installed **MySQL/PostgreSQL** (for metadata storage)

---

## 🔐 3. Setup Passwordless SSH

From **CM node (Edge)** to all other nodes:

```bash
ssh-keygen
ssh-copy-id user@nodeX


🗃️ 4. External Databases Setup
Created databases and users for:

Cloudera Manager (scm)

Hive Metastore (hive)

Oozie (oozie)

Ranger Admin (rangeradmin)

📦 5. Cloudera Tarball Deployment
Downloaded and extracted:
cloudera-manager-el7-cm7.x.x.tar.gz → /opt/cloudera-manager

Setup internal YUM repo using tarball (offline-ready)

Installed:

cloudera-manager-server

cloudera-manager-agent

🔗 6. JDBC Connector Setup
Placed the JDBC connector:

/usr/share/java/mysql-connector-java.jar
or

/usr/share/java/postgresql.jar

🛠️ 7. SCM Database Preparation
Initialized schema:

bash
Copy
Edit
/opt/cloudera/cm/schema/scm_prepare_database.sh mysql scm scm scm_password
🚀 8. Start Cloudera Manager
bash
Copy
Edit
systemctl start cloudera-scm-server
systemctl start cloudera-scm-agent
Access UI at: http://<CM-node>:7180
Login: admin / admin

🧩 9. Cluster Installation via Cloudera Manager UI
Added cluster nodes (auto or manual)

Selected services and roles:

HDFS: NameNode, DataNodes

YARN: ResourceManager, NodeManagers

Hive: Metastore, HiveServer2

Kafka, HBase, Spark, Hue, Oozie, ZooKeeper

Distributed parcels and assigned roles

⚙️ 10. Service Configuration Highlights
HDFS:
Configured NN/DN directories

Formatted NameNode

Hive:
Integrated external MySQL/Postgres metastore

Configured JDBC driver and connection

YARN:
Tuned container memory & resource settings

Kafka:
Configured broker ID, listeners, ZooKeeper connect

HBase:
Set root directory path and ZK quorum

ZooKeeper:
Ensured quorum and port bindings

🔐 11. Security Setup
(Optional but Enterprise-Ready)
Kerberos: Setup using MIT KDC or AD for authentication

Ranger: Centralized authorization and auditing

LDAP/AD Integration: External user/group access control

TLS/SSL: Secured CM UI and other web UIs (optional)

📡 12. Ingestion Pipelines
✅ Real-Time:
Kafka → HDFS → Hive
(via NiFi / Spark Structured Streaming)

✅ Batch:
Sqoop → Hive

HDFS → Spark batch processing jobs

📋 13. Daily Admin Practice
Start/stop services via CM UI & CLI

Add/remove nodes from cluster

Monitor logs, health checks

Configure email alerting

Perform service recovery simulations

💾 14. Backup & Restore Strategies
Hive Metastore DB backups

HDFS fsimage backups

Cloudera configuration export

Ranger policies exported as JSON

🧠 15. Documentation Assets
To include in repo:

✅ Architecture Diagram (architecture.png)

✅ IP & Hostname Mapping Sheet (hosts-config.md)

✅ Port Reference Sheet (ports.md)

✅ Service Layout / Role Mapping

✅ SOPs: Install / Start / Stop / Scale / Secure

🎯 Skills Demonstrated
Area	What You'll Master
Installation	Manual enterprise-style Cloudera setup
Configuration	Full-stack tuning (HDFS, Hive, Kafka, YARN)
Security	Kerberos, Ranger, LDAP
Networking	Host resolution, listeners, ZK quorum setup
Tuning	JVM and container tuning for YARN/Spark
Ingestion	Kafka, NiFi, Sqoop pipelines
Monitoring	Cloudera Manager, health checks, alerting

📂 Repository Structure (Suggested)
pgsql
Copy
Edit
cloudera-admin-deployment/
├── README.md
├── architecture.png
├── hosts-config.md
├── ports.md
├── sops/
│   ├── install.md
│   ├── start-stop.md
│   ├── scale.md
│   └── security.md
├── nifi-templates/
├── hive/
│   └── create-metastore.sql
├── ranger/
│   └── policy-export.json


👨‍💻 Author
Name: Farhan
Role: Big Data Platform Engineer / Cloudera Admin
LinkedIn: [Your LinkedIn URL]
GitHub: [Your GitHub Profile]

