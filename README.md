# Multi-Environment Web Infrastructure (Staging & Production)

## 📌 Project Overview
This project demonstrates the design and implementation of a multi-environment web infrastructure on a single AWS EC2 instance. The primary goal is to securely isolate **Staging** and **Production** environments using port-based Virtual Hosting, manage network traffic via AWS Security Groups, and configure persistent storage using partitioned AWS EBS volumes.

> **Note:** The HTML files in this repository serve as dummy applications to demonstrate successful routing and isolation between environments. The core focus of this project is the **Cloud Infrastructure and Linux Administration**.

## 🚀 Technologies & Tools
- **Cloud Provider:** AWS (EC2, EBS, Security Groups)
- **OS:** Amazon Linux 2023
- **Web Server:** Apache HTTP Server
- **Storage:** XFS File System, `/etc/fstab`
- **Version Control:** Git & GitHub

## 🏗️ Architecture & Features

### 1. Port-Based Virtual Hosting
- Configured Apache to serve two separate environments concurrently on a single EC2 instance.
- **Production Environment:** Listens on port `80` (Mapped to `main` branch).
- **Staging Environment:** Listens on port `8080` (Mapped to `test` branch).

### 2. AWS Security & Traffic Management
- Hardened the server by configuring strict AWS Security Groups inbound rules:
  - **SSH (Port 22):** Restricted to trusted IP addresses only.
  - **HTTP (Port 80):** Open to the public for Production access.
  - **Custom TCP (Port 8080):** Restricted for internal/testing Staging access.

### 3. Persistent Storage Management (AWS EBS)
- Attached secondary EBS volumes to decouple application data from the OS root volume.
- Partitioned and formatted the attached volumes using the **XFS** filesystem.
- Ensured absolute data persistence across reboots by configuring `/etc/fstab` using volume **UUIDs**.
- **Data Isolation:** Mounted specific volumes to `/data/prod` and `/data/staging` to ensure complete separation of environment data.

## 🌿 Branching Strategy
- `main` branch represents the **Live Production** environment.
- `test` branch represents the **Staging/Test** environment.
