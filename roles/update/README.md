# Update the Proxmox hosts

Run the command in the terminal:
```bash
  # The default inventory is "home".
  ansible-playbook update.yml
  ansible-playbook update.yml -i "inventory/home"
  ansible-playbook update.yml -i "inventory/homelab"
  ansible-playbook update.yml -i "inventory/home" -i "inventory/homelab"
```

# Tasks:

## 1. Update all the packages and remove unused ones.
  1. Run the commands update, upgrade and autoremove.

# Created by:

1. Luciano Sampaio.