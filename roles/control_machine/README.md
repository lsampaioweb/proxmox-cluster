# Setup the control machine to run Ansible scripts

Run the command in the terminal:
```bash
  # -K (--ask-become-pass)
  ansible-playbook control_machine.yml -K
```

# Tasks:

## 1. Install required packages:  

## 2. Add passwords into the Secret Manager:
  1. *proxmox_root_password*. All the hosts will need to have the same root password in order to create the cluster.
  1. *proxmox_smtp_password*. The password that will be used to authenticate when sending email notifications.

# Created by: 

1. Luciano Sampaio.