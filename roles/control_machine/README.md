# Setup the control machine to run Ansible scripts

Run the command in the terminal:
```bash
  02 - Run the playbook.
  # (-K is the same as --ask-become-pass)
  # The default inventory is "home".
  ansible-playbook control_machine.yml -K
  ansible-playbook control_machine.yml -K -i "inventory/home"
  ansible-playbook control_machine.yml -K -i "inventory/homelab"
```

# Tasks:

## 1. Setup DNS.

## 2. Install required packages:

# Created by:

1. Luciano Sampaio.
