# Update Proxmox Hosts

This playbook updates all **Proxmox hosts**, ensuring they have the latest packages while removing unused ones.

#
### 1. Run the Update Playbook

The default **inventory file** is `"inventory/home"`, but you can specify a different one if needed.

```bash
ansible-playbook update.yml
```

Specify an inventory file:

```bash
ansible-playbook update.yml -i "inventory/home"
ansible-playbook update.yml -i "inventory/homelab"
```

Run the playbook for **multiple inventories**:

```bash
ansible-playbook update.yml -i "inventory/home" -i "inventory/homelab"
```

#
### 2. Tasks Performed

### System Updates
- Updates **all installed packages**.
- Removes **unused dependencies** to free up space.

#
### Created by:

1. Luciano Sampaio.
