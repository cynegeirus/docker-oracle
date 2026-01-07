# 🐳 Oracle XE 21c with Docker Compose

This project provides a clean and production-ready setup for running **Oracle Database Express Edition (XE) 21c** using **Docker Compose**.

It is designed to be:

* Easy to run 🚀
* Safe for development & testing 🧪
* Clean and maintainable 🧼

---

## 📦 Requirements

Make sure you have the following installed:

* **Docker** 20+
* **Docker Compose** v2+

Check versions:

```bash
docker --version
docker-compose version
```

---

## 📁 Project Structure

```
.
├── docker-compose.yml
└── README.md
```

---

## ⚙️ Docker Compose Configuration

```yaml
services:
  oracle-xe:
    image: gvenzl/oracle-xe:21-slim
    container_name: oracle-xe
    hostname: oracle-xe
    restart: always

    ports:
      - "1521:1521"   # Oracle Listener

    environment:
      ORACLE_PASSWORD: "ChangeMeStrong!"   # SYS / SYSTEM password
      ORACLE_DATABASE: "XEPDB1"            # Default Pluggable DB
      ORACLE_CHARACTERSET: "AL32UTF8"      # Unicode charset

    volumes:
      - oracle-data:/opt/oracle/oradata

volumes:
  oracle-data:
    name: oracle-xe-data
```

---

## 🚀 Getting Started

### 1️⃣ Start the container

```bash
docker-compose up -d
```

### 2️⃣ Check container status

```bash
docker ps
```

You should see:

```
oracle-xe   Up ...   0.0.0.0:1521->1521/tcp
```

---

## 🔌 Database Connection Info

Use the following details to connect:

| Setting      | Value             |
| ------------ | ----------------- |
| Host         | `localhost`       |
| Port         | `1521`            |
| Service Name | `XEPDB1`          |
| Username     | `SYS`             |
| Password     | `ChangeMeStrong!` |

---

## 💻 Example Connection (SQL*Plus)

```bash
sqlplus sys/ChangeMeStrong!@localhost/XEPDB1
```

---

## 🗄️ Persistent Storage

Database files are stored in a **named Docker volume**:

```
oracle-xe-data
```

This ensures your data survives container restarts and upgrades.

To inspect:

```bash
docker volume inspect oracle-xe-data
```

---

## 🔐 Security Notes

⚠️ **Important:**
Change the default password before using this setup in any shared or production environment.

Recommended:

```yaml
ORACLE_PASSWORD: "Use-A-Strong-And-Unique-Password"
```

---

## 🛠️ Useful Commands

### Stop containers

```bash
docker compose down
```

### Stop and remove everything (⚠️ data will remain)

```bash
docker-compose down --remove-orphans
```

### Remove volume too (⚠️ ALL DATA WILL BE LOST)

```bash
docker volume rm oracle-xe-data
```

---

## 📜 License

This setup uses the community image maintained by **gvenzl**.
Please review Oracle XE license terms before using in production.

---

## Issues, Feature Requests or Support

Please use the Issue > New Issue button to submit issues, feature requests or support issues directly to me. You can also send an e-mail to akin.bicer@outlook.com.tr.
