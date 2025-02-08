# Setup Host Machines

This playbook configures **Proxmox host machines** by setting system settings, installing required packages, and ensuring network configurations.

#
### 1. Run the Host Machines Playbook

The default **inventory file** is `"inventory/home"`, but you can specify a different one if needed.

```bash
ansible-playbook host_machines.yml
```

Specify an inventory file:

```bash
ansible-playbook host_machines.yml -i "inventory/home"
ansible-playbook host_machines.yml -i "inventory/homelab"
```

### 2. Tasks Performed

### System Configuration
- **Sets Brazilian timezone** to `America/Maceio`.
- **Sets up Brazilian NTP servers** for time synchronization.
- **Configures UTF-8 locale** as the system default.
- **Disables IPv6** via GRUB settings.

### Package Management
- Installs required system packages, including:
  - **chrony** (time synchronization)
  - **ethtool** (Wake-on-LAN support)
  - **ifupdown2** (network configuration changes without reboot)
  - **parted** (disk partitioning)
  - **qrencode** (two-factor authentication)
  - **intel-microcode** (fixes CPU vulnerabilities, if applicable)
- Adds **Proxmox non-subscription repositories**.
- Removes **Proxmox enterprise repositories**.

### User Management
- Creates the `usr_ansible` account for Ansible automation.
- Generates a **strong password** and stores it in the **secret manager**.

### Network Configuration
- Ensures **consistent NIC naming** by binding interfaces to MAC addresses.
- Applies **custom network configuration files** to the hosts.

### Cleanup and Reboot
- Removes unnecessary packages.
- Checks if a **reboot is required** and reboots if necessary.

#
### Created by:

1. Luciano Sampaio.
