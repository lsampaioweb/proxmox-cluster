# Update Proxmox Hosts

This playbook updates packages on all **Proxmox hosts** and removes the no-subscription popup.

#
### 1. Run the Update Playbook

Run all commands from the `ansible/` directory.

The default **inventory file** is `"inventory/home"`, but you can specify a different one if needed.

```bash
cd ansible
ansible-playbook 04-update.yml
```

Specify an inventory file:

```bash
cd ansible
ansible-playbook 04-update.yml -i "inventory/home"
ansible-playbook 04-update.yml -i "inventory/homelab"
```

Run the playbook for **multiple inventories**:

```bash
cd ansible
ansible-playbook 04-update.yml -i "inventory/home" -i "inventory/homelab"
```

#
### 2. Tasks Performed

### System Updates
- Updates **all installed packages**.
- Removes the **Proxmox no-subscription popup**.

#
### Created by:

1. Luciano Sampaio.
