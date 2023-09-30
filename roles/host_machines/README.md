# Setup Host Machines

Run the command in the terminal:
```bash
  01 - Save these passwords in the secret manager.
    secret-tool store --label="local-user-password" password local-user-password
    secret-tool store --label="proxmox-root-password" password proxmox-root-password
    secret-tool store --label="proxmox-smtp-password" password proxmox-smtp-password

  02 - Run the playbook.
  ansible-playbook host_machines.yml
```

# Tasks:

## 1. Setup the UTF-8 locale.
  1. Set the locale to UTF-8.

## 2. Setup DNS.
  1. Set the DNS for the host.

## 3. Disable IPV6.
  1. Disable IPV6 by setting GRUB_CMDLINE_LINUX="ipv6.disable=1".

## 4. Install required packages.
  1. Install required packages.

## 5. Remove unnecessary packages.
  1. Remove unnecessary packages.

## 6. Setup Brazilian timezone.
  1. Set the timezone to America/Maceio.

## 7. Setup Brazilian NTP Servers.
  1. Set Brazilian NTP servers.

## 8. Create the Ansible user account:
  1. The **usr_ansible** account is created on each host. This will be the user that Ansible will use to connect and run commands. It must have a very strong password.

## 9. Setup the network interfaces.
  1. Copy the network config file to the host.
  1. Edit the grub file so the network cards (NIC) are named as eth0 - ethX.

# Created by:

1. Luciano Sampaio.