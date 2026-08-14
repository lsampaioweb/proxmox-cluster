# Setup a Proxmox HomeLab using Ansible

This playbook automates the setup of **one or more servers running Proxmox Virtual Environment (PVE) 8.X**.

#
### 1. Store Required Passwords

To avoid repeated password prompts (`-K` for sudo access), store the required credentials securely in the **secret manager**:

### **Local User Password**
Used for privilege escalation (`become`):
```bash
secret-tool store --label="local-user-password" password "local-user-password"
```

Verify:
```bash
secret-tool lookup password "local-user-password"
```

### **Proxmox Root Password**
Used for connecting to the **Proxmox nodes**:
```bash
secret-tool store --label="proxmox-root-password" password "proxmox-root-password"
```

Verify:
```bash
secret-tool lookup password "proxmox-root-password"
```

### **SMTP Password**
Used for **sending email notifications**:
```bash
secret-tool store --label="proxmox-smtp-password" password "proxmox-smtp-password"
```

Verify:
```bash
secret-tool lookup password "proxmox-smtp-password"
```

### 2. Run the Proxmox Setup Playbook

Run all commands from the `ansible/` directory.

The default **inventory file** is `"inventory/home"`, but you can specify a different one if needed.

```bash
cd ansible
ansible-playbook site.yml
```

Specify an inventory file:

```bash
cd ansible
ansible-playbook site.yml -i "inventory/home"
ansible-playbook site.yml -i "inventory/homelab"
```

### 2.1 Run Individual Playbooks

You can also run each playbook independently in sequence:

```bash
cd ansible
ansible-playbook 01-control_machine.yml -i "inventory/home"
ansible-playbook 02-host_machines.yml -i "inventory/home"
ansible-playbook 03-proxmox.yml -i "inventory/home"
ansible-playbook 04-update.yml -i "inventory/home"
```

Or run a specific playbook standalone:

```bash
cd ansible
ansible-playbook 03-proxmox.yml -i "inventory/home"
```

**Note:** `site.yml` orchestrates all four playbooks in sequence. Use `site.yml` for full end-to-end setup, or run individual playbooks if you need to re-run a specific configuration step.

### 3. Roles You Can Execute

1. [Setup](ansible/roles/control_machine/README.md) the **control machine** to run Ansible scripts.
2. [Setup](ansible/roles/host_machines/README.md) each **Proxmox machine**.
3. [Setup](ansible/roles/proxmox/README.md) **Proxmox** as a cluster.
4. [Update](ansible/roles/update/README.md) the **Proxmox nodes**.

### 4. Additional Resources

[Useful Links](links.md "Links")

### License

This project is licensed under the [MIT License](LICENSE).

#
### Created by

1. Luciano Sampaio.
