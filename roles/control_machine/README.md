# Setup the Control Machine for Ansible

This playbook configures the **control machine** to run Ansible scripts by setting up DNS and installing required packages.

#
### 1. Run the Control Machine Playbook

The default **inventory file** is `"inventory/home"`, but you can specify a different one if needed.

```bash
ansible-playbook control_machine.yml
```

Specify an inventory file:

```bash
ansible-playbook control_machine.yml -i "inventory/home"
ansible-playbook control_machine.yml -i "inventory/homelab"
```

### 2. Tasks Performed

### DNS Configuration
- Copies a **custom DNS configuration file** (`/etc/resolv.conf`).

### Package Installation
- Installs required system packages:
  - **sshpass** (for SSH automation)
  - **libsecret-tools** (for password management)
  - **python-is-python3** (ensures `python` command points to Python 3)
  - **pipx** (for managing Python packages)
  - **python3-passlib** (for password hashing)
  - **python3-jmespath** (for JSON queries in Ansible)
- Installs **Ansible** and **Ansible Lint** via `pipx`.
- Injects **passlib** into the Ansible environment.

#
### Created by:

1. Luciano Sampaio.
