# Setup the control machine to run Ansible scripts

Run the command in the terminal:
```bash
  01 - Save these passwords in the secret manager.
    secret-tool store --label="local_user_password" password local_user_password
    secret-tool store --label="proxmox_root_password" password proxmox_root_password
    secret-tool store --label="proxmox_smtp_password" password proxmox_smtp_password

  02 - Run the playbook.
  ansible-playbook control_machine.yml
```

# Tasks:

## 1. Install required packages:  

# Created by: 

1. Luciano Sampaio.