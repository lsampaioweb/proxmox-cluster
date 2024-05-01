# Setup a Proxmox HomeLab using Ansible

The playbook can setup one or more servers running Proxmox Virtual Environment (PVE) 7.1.

Run the command in the terminal:
```bash
# 01 - Save these passwords in the secret manager.
# It will avoid the need to type -K (ask the become password).
secret-tool store --label="local-user-password" password "local-user-password"
# Verify the command worked.
secret-tool lookup password "local-user-password"

# It will be used to connect to the Proxmox nodes.
secret-tool store --label="proxmox-root-password" password "proxmox-root-password"
# Verify the command worked.
secret-tool lookup password "proxmox-root-password"

# It will be used to send emails.
secret-tool store --label="proxmox-smtp-password" password "proxmox-smtp-password"
# Verify the command worked.
secret-tool lookup password "proxmox-smtp-password"

# The default inventory is "inventory/home".
ansible-playbook site.yml
ansible-playbook site.yml -i "inventory/home"
ansible-playbook site.yml -i "inventory/homelab"
```

#
### Roles you can execute:
1. [Setup](roles/control_machine/README.md) the control machine to run Ansible scripts.
1. [Setup](roles/host_machines/README.md) the host machines.
1. [Setup](roles/proxmox/README.md) Proxmox.

#
### Links:

[Links](links.md "Links")

#
### License:

[MIT](LICENSE "MIT License")

#
### Created by:

1. Luciano Sampaio.
