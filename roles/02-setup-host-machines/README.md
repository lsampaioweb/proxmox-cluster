# Setup Host Machines

Run the command in the terminal:
```bash
  ansible-playbook 02-setup-host-machines.yml
```

# Tasks:

## 1. Disable IPV6.
  1. Disable IPV6 by setting GRUB_CMDLINE_LINUX_DEFAULT="ipv6.disable=1".

## 2. Remove unnecessary packages.
  1. Remove unnecessary packages.

## 3. Install required packages.
  1. Install required packages.

## 4. Setup Brazilian timezone.
  1. Set the timezone to America/Maceio.

## 5. Setup Brazilian NTP Servers.
  1. Set Brazilian NTP servers.

## 6. Create the Ansible user account:
  1. The **usr_ansible** account is created on each host. This will be the user that Ansible will use to connect and run commands. It must have a very strong password.

## 7. Setup the network interfaces.
  1. Copy the network config file to the host.
  1. Edit the grub file so the network cards (NIC) are named as eth0 - ethX.

# Created by: 

1. Luciano Sampaio.