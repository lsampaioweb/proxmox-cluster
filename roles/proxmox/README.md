# Setup Proxmox Cluster

This playbook automates the configuration of a **Proxmox cluster**, including **email notifications, cluster creation, network settings, storage management, and resource allocation**.

#
### 1. Run the Proxmox Playbook

The default **inventory file** is `"inventory/home"`, but you can specify a different one if needed.

```bash
ansible-playbook proxmox.yml
```

Specify an inventory file:

```bash
ansible-playbook proxmox.yml -i "inventory/home"
ansible-playbook proxmox.yml -i "inventory/homelab"
```

### 2. Tasks Performed

### Email Notifications
- Configures **Postfix** for email alerts.
- Stores **SMTP credentials** in the `sasl_passwd` file.
- Updates **relayhost** and **SASL authentication settings** in `main.cf`.

### Remove No Subscription Popup
- Disables the **Proxmox subscription warning**.

### Cluster Configuration
- **Creates the Proxmox cluster** and joins additional nodes.
- Adds **host fingerprints** to `~/.ssh/known_hosts` for secure communication.

### Migration Network Setup
- Defines **a dedicated network for Proxmox migrations** in `/etc/pve/datacenter.cfg`.

### Storage Management
- Formats **HDD, SSD, and NVMe disks**:
  - Extends the **data partition** to 100% of available space.
  - Removes **old partitions**.
  - Creates **new partitions, volume groups, and logical volumes**.

### Resource Management
- Creates **resource pools** (`Template`, `Staging`, `Production`).
- Defines **custom roles** (e.g., `Packer`).
- Configures **High Availability (HA) groups**.

### Ceph Storage Cleanup
If Ceph is installed and needs to be removed, the following commands **purge Ceph storage**:

```bash
systemctl stop ceph-mon.target
systemctl stop ceph-mgr.target
systemctl stop ceph-mds.target
systemctl stop ceph-osd.target
systemctl stop ceph.target
systemctl stop ceph-crash.service
rm -rf /etc/systemd/system/ceph*
killall -9 ceph-mon ceph-mgr ceph-mds
rm -rf /var/lib/ceph/*
pveceph purge
apt-get purge ceph-mon ceph-mgr ceph-mds ceph-osd -y
apt-get purge ceph-base ceph-mgr-modules-core -y
rm -rf /etc/ceph/* /etc/pve/ceph.conf /etc/pve/priv/ceph.*
apt-get autoremove -y
lvremove -y /dev/ceph*
vgremove -y ceph- <tab>
pvremove /dev/nvme0n1
touch '/please-remove-proxmox-ve'
apt remove -y proxmox-ve
apt autoremove -y
apt install -y proxmox-ve
```

#
### Created by:

1. Luciano Sampaio.