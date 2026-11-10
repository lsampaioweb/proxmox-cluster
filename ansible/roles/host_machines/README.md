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

### 1.1 Update Network Configuration Only

For already provisioned nodes, run `06-host-network.yml` to apply network changes without rerunning package installation, user management, or other host setup tasks. It imports only `host_machines/tasks/network.yml`, retaining the role variables, templates, and handlers from the `common` dependency.

The nodes must already have the required packages, including `ifupdown2`, installed. SSH access, host fingerprints in the control machine's `known_hosts`, and the configured secret-manager credentials must already be available.

From the `ansible/` directory, select the inventory matching the network template and host variables:

```bash
ansible-playbook 06-host-network.yml -i "inventory/home"
ansible-playbook 06-host-network.yml -i "inventory/homelab"
```

To update only one node:

```bash
ansible-playbook 06-host-network.yml -i "inventory/homelab" --limit "pve-01.lan.homelab"
```

Update the inventory-specific interface template or relevant host variables before running the playbook. Changes to `/etc/network/interfaces` trigger `ifreload -a` and a connection wait; changes to NIC naming rules can trigger a reboot. Management-network changes can interrupt access.

The playbook does not set `serial`, so it does not enforce one-node-at-a-time updates. Use `--limit` and separate runs when applying changes node by node. This standalone playbook is not included in `site.yml`.

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
