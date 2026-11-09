# Setup Host Machines

This playbook configures **Proxmox host machines** by setting system settings, installing required packages, and ensuring network configurations.

#
### 1. Run the Host Machines Playbook

Run all commands from the `ansible/` directory.

The default **inventory file** is `"inventory/home"`, but you can specify a different one if needed.

```bash
cd ansible
ansible-playbook 02-host-machines.yml
```

Specify an inventory file:

```bash
cd ansible
ansible-playbook 02-host-machines.yml -i "inventory/home"
ansible-playbook 02-host-machines.yml -i "inventory/homelab"
```

### 2. Tasks Performed

### System Configuration
- **Sets Brazilian timezone** to `America/Maceio`.
- **Configures an inventory-specific NTP pool** (`ntp-pool.<domain>`) for time synchronization.
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
- Adds the **Proxmox no-subscription repository** for the host's Debian release, signed with the Proxmox archive keyring.
- Removes **Proxmox enterprise repositories**.

### User Management
- Creates the `usr_ansible` account for Ansible automation.
- Generates a **strong password** and stores it in the **secret manager**.

### Network Configuration
- Ensures **consistent NIC naming** by binding interfaces to MAC addresses.
- Renders **inventory-specific management, cluster, and VM bridge configuration** from host variables.

### Cleanup and Reboot
- Removes unnecessary packages.
- Checks if a **reboot is required** and reboots if necessary.

#
### Created by:

1. Luciano Sampaio.
