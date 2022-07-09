# Setup the control machine to run Ansible scripts

Run the command in the terminal:
```bash
  ansible-playbook 01-setup-control-machine.yml -K (--ask-become-pass)
```

# Tasks:

## 1. Install required packages:
  1. **SSH Pass**. It allows you to provide the ssh password without using the prompt. This will be necessary for the first settings when we don't have a SSH keypair yet.

## 2. Add the IP and URL of each host into the /etc/hosts file:
    10.0.3.5 kvm-01.homelab kvm-01
    10.0.3.6 kvm-02.homelab kvm-02
    10.0.3.7 kvm-03.homelab kvm-03
    10.0.3.8 kvm-04.homelab kvm-04
    10.0.3.9 kvm-05.homelab kvm-05
    10.0.3.10 kvm-06.homelab kvm-06

## 3. Add the fingerprint of each host into the ~/.ssh/known_hosts file:
    kvm-01.homelab,kvm-01,10.0.3.5 ecdsa-sha2-nistp256 ...
    kvm-02.homelab,kvm-02,10.0.3.6 ecdsa-sha2-nistp256 ...
    kvm-03.homelab,kvm-03,10.0.3.7 ecdsa-sha2-nistp256 ...
    kvm-04.homelab,kvm-04,10.0.3.8 ecdsa-sha2-nistp256 ...
    kvm-05.homelab,kvm-05,10.0.3.9 ecdsa-sha2-nistp256 ...
    kvm-06.homelab,kvm-06,10.0.3.10 ecdsa-sha2-nistp256 ...

## 4. Add passwords into the Secret Manager:
  1. *proxmox-root-password*. All the hosts will need to have the same root password in order to create the cluster.
  1. *proxmox-smtp-password*. The password that will be used to authenticate when sending email notifications.

# Created by: 

1. Luciano Sampaio.