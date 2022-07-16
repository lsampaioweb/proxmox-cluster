# Setup a Proxmox HomeLab using Ansible

The playbook can setup one or more servers running Proxmox Virtual Environment (PVE) 7.1.

Run the command in the terminal:
```bash
  ansible-playbook site.yml -K
```

# Roles you can execute:
1. [Setup](roles/01-setup-control-machine/README.md) the control machine to run Ansible scripts.
1. [Setup](roles/02-setup-host-machines/README.md) the host machines.
1. [Setup](roles/03-setup-proxmox/README.md) Proxmox.

# Links:

[Links](links.md "Links")

# License:

[MIT](LICENSE "MIT License")

# Created by: 

1. Luciano Sampaio.
