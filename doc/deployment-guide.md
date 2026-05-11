# VMware vSphere Infrastructure Deployment Guide

---

# 1. Introduction

This guide explains the deployment and configuration process of a VMware vSphere infrastructure lab environment using VMware Workstation.

The environment includes:

- VMware ESXi Hosts
- VMware vCenter Server Appliance (VCSA)
- Shared NFS Storage
- vMotion
- High Availability (HA)
- Distributed Resource Scheduler (DRS)
- Fault Tolerance (FT)

---

# 2. Lab Environment

## Hardware Requirements

Recommended minimum system requirements:

| Component | Requirement |
|----------|-------------|
| CPU | Intel i5/i7 with virtualization support |
| RAM | 16 GB minimum (32 GB recommended) |
| Storage | 200 GB SSD recommended |
| Network | Virtual NAT or Bridged Network |

---

# 3. Software Requirements

| Software | Version |
|----------|---------|
| VMware Workstation | 17 Pro |
| VMware ESXi | 7.x |
| VMware vCenter Server Appliance | 7.x |
| CentOS | 7 / 8 |

---

# 4. Network Design

## Network Segments

| Network Type | Purpose |
|--------------|---------|
| Management Network | ESXi & vCenter management |
| vMotion Network | VM live migration |
| Storage Network | NFS datastore communication |
| VM Network | Virtual machine traffic |

---

# 5. ESXi Host Deployment

## Step 1 — Create ESXi Virtual Machines

Inside VMware Workstation:

- Create two virtual machines
- Select VMware ESXi ISO
- Allocate resources:
  - 4 vCPUs
  - 8 GB RAM
  - 100 GB Disk

Example:

| Hostname | IP Address |
|----------|------------|
| ESXi-01 | 192.168.137.106 |
| ESXi-02 | 192.168.137.107 |

---

## Step 2 — Install ESXi

1. Boot from ESXi ISO
2. Start installation wizard
3. Select storage disk
4. Configure root password
5. Complete installation
6. Reboot host

---

## Step 3 — Configure Management Network

After installation:

- Configure static IP address
- Configure subnet mask
- Configure gateway
- Configure DNS server

Verify network connectivity using:

```bash
ping <gateway-ip>
```

---

# 6. vCenter Server Deployment

## Step 1 — Deploy VCSA

1. Mount VCSA ISO
2. Launch installer
3. Select:
   - Deploy vCenter Server
4. Enter ESXi target host information
5. Configure:
   - Appliance name
   - Root password
   - Network settings

---

## Step 2 — Complete vCenter Setup

Configure:

- SSO domain
- Administrator account
- Time synchronization
- CEIP settings

Access vCenter using:

```txt
https://<vcenter-ip>
```

---

# 7. Cluster Configuration

## Step 1 — Create Datacenter

Inside vCenter:

- Create new Datacenter
- Name the datacenter

---

## Step 2 — Create Cluster

Enable:

- vSphere HA
- vSphere DRS

Add both ESXi hosts to the cluster.

---

# 8. Virtual Networking Configuration

## Configure vSwitches

Create:

| vSwitch | Purpose |
|---------|---------|
| vSwitch0 | Management & VM Network |
| vSwitch1 | vMotion & Storage |

---

## Configure Port Groups

Create port groups:

- Management Network
- VM Network
- vMotion Network
- Storage Network

---

## Configure VMkernel Adapters

Assign VMkernel adapters for:

- Management
- vMotion
- Storage

Enable vMotion service on the vMotion VMkernel adapter.

---

# 9. Shared Storage Configuration

## Step 1 — Configure NFS Server

On CentOS:

Install NFS utilities:

```bash
yum install nfs-utils -y
```

Create shared directory:

```bash
mkdir /nfs-share
```

Edit exports file:

```bash
nano /etc/exports
```

Add:

```txt
/nfs-share *(rw,sync,no_root_squash)
```

Restart NFS service:

```bash
systemctl restart nfs-server
```

---

## Step 2 — Add NFS Datastore to vSphere

Inside vCenter:

1. Open Storage
2. Create New Datastore
3. Select NFS
4. Enter:
   - NFS Server IP
   - Shared Folder Path
   - Datastore Name

Verify datastore accessibility from both ESXi hosts.

---

# 10. Virtual Machine Operations

## Snapshot Management

Create VM snapshots before major changes.

Steps:

1. Right-click VM
2. Snapshots
3. Take Snapshot

---

## Clone Virtual Machine

1. Right-click VM
2. Clone
3. Select target host and datastore

---

## Convert VM to Template

1. Right-click VM
2. Clone to Template

Templates allow rapid deployment of new VMs.

---

# 11. vMotion Configuration

## Requirements

- Shared storage
- VMkernel vMotion network
- Compatible CPUs
- Proper licensing

---

## Test vMotion

1. Right-click VM
2. Migrate
3. Select:
   - Change compute resource only
4. Choose destination host

Verify live migration without downtime.

---

# 12. High Availability (HA)

## Enable HA

Inside Cluster Settings:

- Enable vSphere HA
- Configure admission control

---

## Test HA

1. Power off one ESXi host
2. Observe VM restart on surviving host

Expected Result:

- Automatic VM failover
- Reduced downtime

---

# 13. Distributed Resource Scheduler (DRS)

## Enable DRS

Cluster Settings:

- Enable DRS
- Set automation level to Fully Automated

---

## Test DRS

Generate load on one host.

Expected behavior:

- Automatic VM migration
- Balanced CPU & memory utilization

---

# 14. Fault Tolerance (FT)

## Requirements

- Shared storage
- vMotion enabled
- FT logging network
- Compatible CPUs

---

## Enable FT

1. Right-click VM
2. Fault Tolerance
3. Turn On Fault Tolerance

---

## Test FT

Power off primary ESXi host.

Expected behavior:

- Secondary VM continues operation instantly
- No service interruption

---

# 15. Troubleshooting

| Issue | Solution |
|------|----------|
| vMotion failed | Verify VMkernel configuration |
| HA not working | Check shared storage access |
| FT unsupported | Verify CPU compatibility |
| Datastore inaccessible | Check NFS exports and firewall |

---

# 16. Conclusion

This project successfully demonstrates the deployment and management of a VMware vSphere enterprise virtualization infrastructure.

The lab environment provides practical experience with:

- ESXi administration
- vCenter management
- Cluster services
- Enterprise virtualization technologies
- Storage and networking
- High availability and disaster recovery concepts

The implementation of HA, DRS, vMotion, and FT simulates real-world enterprise virtualization environments and improves infrastructure reliability, scalability, and performance.
