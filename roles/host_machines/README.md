# Setup Host Machines

Run the command in the terminal:
```bash
  01 - Save these passwords in the secret manager.
    # It will avoid the need to type -K (ask the become password).
    secret-tool store --label="local-user-password" password local-user-password
    # It will be used to connect to the Proxmox nodes.
    secret-tool store --label="proxmox-root-password" password proxmox-root-password
    # It will be used to send emails.
    secret-tool store --label="proxmox-smtp-password" password proxmox-smtp-password

  02 - Run the playbook.
    # The default inventory is "home".
    ansible-playbook host_machines.yml
    ansible-playbook host_machines.yml -i "inventory/home"
    ansible-playbook host_machines.yml -i "inventory/homelab"
```

# Tasks:

## 1. Setup Brazilian timezone.
  1. Set the timezone to America/Maceio.

## 2. Setup the UTF-8 locale.
  1. Set the locale to UTF-8.

## 3. Install required packages.
  1. Install required packages.

## 4. Setup Brazilian NTP Servers.
  1. Set Brazilian NTP servers.

## 5. Create the Ansible user account:
  1. The **usr_ansible** account is created on each host. This will be the user that Ansible will use to connect and run commands. It must have a very strong password.

## 6. Disable IPV6.
  1. Disable IPV6 by setting GRUB_CMDLINE_LINUX="ipv6.disable=1".

## 7. Setup the network interfaces.
  1. Copy the network config file to the host.
  1. Edit the grub file so the network cards (NIC) are named as eth0 - ethX.

## 8. Remove unnecessary packages.
  1. Remove unnecessary packages.

# Created by:

1. Luciano Sampaio.
