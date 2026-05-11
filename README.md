# VMware vSphere Infrastructure Deployment

![VMware](https://img.shields.io/badge/VMware-vSphere-orange)
![ESXi](https://img.shields.io/badge/ESXi-Hosts-blue)
![vCenter](https://img.shields.io/badge/vCenter-Server-success)
![HA](https://img.shields.io/badge/High_Availability-Enabled-brightgreen)
![DRS](https://img.shields.io/badge/DRS-Configured-blueviolet)
![FT](https://img.shields.io/badge/Fault_Tolerance-Active-red)
![License](https://img.shields.io/badge/License-MIT-yellow)

---

# VMware vSphere Infrastructure Deployment

## Project Overview

This project demonstrates the deployment and configuration of a complete VMware vSphere infrastructure within a virtual lab environment using VMware Workstation.

The environment simulates a real enterprise virtualization infrastructure that includes centralized management, shared storage, workload balancing, high availability, and fault tolerance capabilities.

The project was designed to provide hands-on experience with VMware enterprise technologies and infrastructure management.

---

# Infrastructure Components

- 2 VMware ESXi Hosts
- VMware vCenter Server Appliance (VCSA)
- Shared NFS Storage
- VMware Standard vSwitches
- VMkernel Adapters
- Port Groups
- Windows/Linux Virtual Machines

---

# Implemented Features

## vMotion
Live migration of virtual machines between ESXi hosts without downtime.

## High Availability (HA)
Automatic restart of virtual machines after ESXi host failure.

## Distributed Resource Scheduler (DRS)
Automatic workload balancing across ESXi hosts based on CPU and memory utilization.

## Fault Tolerance (FT)
Continuous virtual machine availability using synchronized secondary VM replication.

## Shared Storage
NFS shared datastore configuration for cluster services and VM accessibility.

## Virtual Networking
Configuration of:
- vSwitches
- VMkernel adapters
- Port groups
- Management network
- vMotion network
- Storage network

---

# Architecture Diagram

![Architecture](docs/architecture-diagram.png)

---

# Project Structure

```bash
docs/
networking/
storage/
cluster/
vm-operations/
```

---

# Screenshots

## vCenter Dashboard
![vCenter](docs/screenshots/vcenter-dashboard.png)

## Cluster Configuration
![Cluster](docs/screenshots/cluster-configuration.png)

## vMotion Migration
![vMotion](docs/screenshots/vmotion.png)

## High Availability Testing
![HA](docs/screenshots/ha-testing.png)

## Distributed Resource Scheduler
![DRS](docs/screenshots/drs.png)

## Fault Tolerance
![FT](docs/screenshots/fault-tolerance.png)

---

# Technologies Used

- VMware Workstation
- VMware ESXi
- VMware vCenter Server
- VMware vSphere
- NFS Storage
- CentOS
- Virtual Networking

---

# Learning Outcomes

Through this project, the following skills were developed:

- VMware vSphere deployment and management
- ESXi installation and configuration
- vCenter administration
- Cluster management
- Shared storage configuration
- Enterprise virtual networking
- High availability implementation
- VM migration and workload balancing
- Fault tolerance configuration
- Infrastructure troubleshooting

---

# Team Members

- Abdelaziz Mohamed
- Kareem El-Guishy
- Mohamed Gamal
- Mai Wael

---

# Supervised By

Eng. Ekram Abdelwahab

---
