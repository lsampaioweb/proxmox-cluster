# Setup a Proxmox HomeLab using Ansible

The playbook can setup one or more servers running Proxmox Virtual Environment (PVE) 7.1.

Run the command in the terminal:
```bash
  # (-K is the same as --ask-become-pass)
  # The default inventory is "home".
  ansible-playbook site.yml -K
  ansible-playbook site.yml -K -i "inventory/home"
  ansible-playbook site.yml -K -i "inventory/homelab"
```

# Roles you can execute:
1. [Setup](roles/control_machine/README.md) the control machine to run Ansible scripts.
1. [Setup](roles/host_machines/README.md) the host machines.
1. [Setup](roles/proxmox/README.md) Proxmox.

# Links:

[Links](links.md "Links")

# License:

[MIT](LICENSE "MIT License")

# Created by:

1. Luciano Sampaio.
