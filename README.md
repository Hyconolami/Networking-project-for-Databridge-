# 🧠 Networking Project for Databridge Innovations
**Module:** Network Design and Security (Cisco Packet Tracer Lab)  
**Assignment Title:** Configuring ACLs to Secure Multi-Department Network  
**Author:** Hammed Olamilekan Yakub  
**Date:** 31 October 2025  

---

## 📘 Project Overview

This project demonstrates how to enhance **network security in a multi-department environment** using **Access Control Lists (ACLs)** on a Cisco router.

The goal was to ensure that only **authorized departments** (Admin and Sales) can access the **Admin Server (HTTP)** while blocking unauthorized departments (HR). This configuration enforces internal network segmentation, data security, and controlled communication between departments.

---

## 🧩 Network Topology Summary

**Router: Databridge**  
- **Gi0/0 – 192.168.10.1/24 (Admin)**  
- **Gi0/1 – 192.168.20.1/24 (Sales)**  
- **Gi0/2 – 192.168.30.1/24 (HR)**  

**Admin Network**
- Admin-Server: `192.168.10.5` (HTTP ON, Gateway 192.168.10.1)  
- Admin-PC1: `192.168.10.10`  
- Admin-PC2: `192.168.10.11`

**Sales Network**
- Sales-PC1: `192.168.20.10`  
- Sales-PC2: `192.168.20.11`

**HR Network**
- HR-PC1: `192.168.30.10`  
- HR-PC2: `192.168.30.11`

---

## 🔐 ACL Configuration

### Access Control List Name: `HTTP_ACCESS`
**Applied:** Inbound on Gi0/0  
**Purpose:** Allow Admin and Sales access to the Admin server (HTTP), deny HR.  

```bash
Databridge> enable
Databridge# configure terminal
Databridge(config)# ip access-list extended HTTP_ACCESS
Databridge(config-ext-nacl)# permit tcp 192.168.10.0 0.0.0.255 host 192.168.10.5 eq 80
Databridge(config-ext-nacl)# permit tcp 192.168.20.0 0.0.0.255 host 192.168.10.5 eq 80
Databridge(config-ext-nacl)# deny ip 192.168.30.0 0.0.0.255 host 192.168.10.5
Databridge(config-ext-nacl)# exit
Databridge(config)# interface Gig0/0
Databridge(config-if)# ip access-group HTTP_ACCESS in
Databridge(config-if)# exit
Databridge(config)# end

