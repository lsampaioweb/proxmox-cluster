# Setup the control machine to run Ansible scripts

Run the command in the terminal:
```bash
  ansible-playbook 01-setup-control-machine.yml --ask-become-pass (or -K)
```

# Tasks:

## 1. Install required packages:
  1. **SSH Pass**. It allows you to provide the ssh password without using the prompt. This will be necessary for the first settings when we don't have a SSH keypair yet.

## 2. Add the IP and URL of each host into the /etc/hosts file:
    192.168.0.21 host01.aprendendo.com.br host01
    192.168.0.22 host02.aprendendo.com.br host02
    192.168.0.23 host03.aprendendo.com.br host03

## 3. Add the fingerprint of each host into the ~/.ssh/known_hosts file:
    host01.aprendendo.com.br,host01,192.168.0.21 ecdsa-sha2-nistp256 ...
    host02.aprendendo.com.br,host02,192.168.0.22 ecdsa-sha2-nistp256 ...
    host03.aprendendo.com.br,host03,192.168.0.23 ecdsa-sha2-nistp256 ...

## 4. Add passwords into the Secret Manager (Keychain):
  1. *proxmox-root-password*. All the hosts will need to have the same root password in order to create the cluster.
  1. *proxmox-smtp-password*. The password that will be used to authenticate when sending email notifications.

# Created by: 

1. Luciano Sampaio.