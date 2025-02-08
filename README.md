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

The default **inventory file** is `"inventory/home"`, but you can specify a different one if needed.

```bash
ansible-playbook site.yml
```

Specify an inventory file:

```bash
ansible-playbook site.yml -i "inventory/home"
ansible-playbook site.yml -i "inventory/homelab"
```

### 3. Roles You Can Execute

1. [Setup](roles/control_machine/README.md) the **control machine** to run Ansible scripts.
2. [Setup](roles/host_machines/README.md) each **Proxmox machine**.
3. [Setup](roles/proxmox/README.md) **Proxmox** as a cluster.
4. [Update](roles/update/README.md) the **Proxmox nodes**.

### 4. Additional Resources

[Useful Links](links.md "Links")

### License

This project is licensed under the [MIT License](LICENSE).

#
### Created by

- **Luciano Sampaio**
