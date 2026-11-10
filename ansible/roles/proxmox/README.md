# Setup Proxmox Cluster

This playbook automates the configuration of a **Proxmox cluster**, including **email notifications, cluster creation, network settings, storage management, and resource allocation**.

#
### 1. Run the Proxmox Playbook

Run all commands from the `ansible/` directory.

The default **inventory file** is `"inventory/home"`, but you can specify a different one if needed.

```bash
cd ansible
ansible-playbook 03-proxmox.yml
```

Specify an inventory file:

```bash
cd ansible
ansible-playbook 03-proxmox.yml -i "inventory/home"
ansible-playbook 03-proxmox.yml -i "inventory/homelab"
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
- For the Home inventory, Corosync Link 0 uses `172.16.11.0/28`; Link 1 uses the management addresses on VLAN 1110 (`10.1.10.0/28`).
- Cluster creation is skipped when `/etc/pve/corosync.conf` already exists. Rerunning `03-proxmox.yml` does not change Corosync link addresses on an existing cluster.
- Adds **host fingerprints** to `~/.ssh/known_hosts` for secure communication.

### WebUI Certificate
- Store each inventory domain's `pve.<domain>.crt` and matching unencrypted `pve.<domain>.key` under `roles/proxmox/files/certificates/<domain>/`.
- The certificate is installed on each node after cluster setup. Re-run `05-proxmox-certificates.yml` with the selected inventory after renewing it.

```bash
cd ansible
ansible-playbook 05-proxmox-certificates.yml -i inventory/home
ansible-playbook 05-proxmox-certificates.yml -i inventory/homelab
```

### Migration Network Setup
- Defines **the migration network** in `/etc/pve/datacenter.cfg`. In the Home inventory this is `172.16.12.0/28`, the same subnet used by Ceph.
- The datacenter configuration is rendered from `datacenter.cfg.j2` on each run. Keep settings that must persist in that template and its inventory variables; settings added only through the WebUI can be replaced.

### Storage Management
- Formats **HDD, SSD, and NVMe disks**:
  - Extends the **data partition** to 100% of available space.
  - Removes **old partitions**.
  - Creates **new partitions, volume groups, and logical volumes**.

### Ceph Storage
- Adds the **Ceph Tentacle no-subscription repository** for the host's Debian release, signed with the Proxmox archive keyring.
- Initializes Ceph on the configured **Ceph network**. For Home, that is `172.16.12.0/28`; the host network playbook assigns this subnet to `enp2lacp1` at MTU 9000.
- Creates monitors, managers, MDSs, OSDs, CRUSH rules, CephFS, and pools from the inventory variables. Home uses `pve-01.lan.home` as the Ceph master; homelab uses `pve-04.lan.homelab`.
- The Home pools use replica size 2 and `min_size` 1. This keeps I/O available after one OSD is lost but leaves data without redundancy until the OSD is restored.

### Resource Management
- Creates **resource pools** (`Template`, `Staging`, `Production`).
- Defines **custom roles** (e.g., `Packer`).
- HA resource and affinity rule configuration is deferred until VM/CT IDs and placement requirements are defined.

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