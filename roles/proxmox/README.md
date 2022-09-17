# Setup Proxmox

Run the command in the terminal:
```bash
  ansible-playbook 03-setup-proxmox.yml
```

# Tasks:

## 1. Add the internal IP and name of all hosts into the 'hosts' file.
  1. Add the internal IP and url of all hosts into the 'hosts' file.

## 2. Setup email notification with Postfix.
  1. Add the SMTP server, user name and password into the sasl_passwd file.
  1. Add relayhost into the main.cf file.
  1. Add SASL authentication into the main.cf file.

## 3. Remove the no subscription popup.
  1. Replace the verification with a if (false).

## 4. Create the cluster and join the nodes into it.
  1. Create the cluster.
  1. Add nodes to the cluster.
  1. Add the fingerprint of each host into the ~/.ssh/known_hosts file:
  ```bash
    kvm-01.homelab ecdsa-sha2-nistp256 ...
    kvm-02.homelab ecdsa-sha2-nistp256 ...
    kvm-03.homelab ecdsa-sha2-nistp256 ...
    kvm-04.homelab ecdsa-sha2-nistp256 ...
    kvm-05.homelab ecdsa-sha2-nistp256 ...
    kvm-06.homelab ecdsa-sha2-nistp256 ...
    kvm-07.homelab ecdsa-sha2-nistp256 ...
  ```

## 5. Set the network for all migrations in the cluster.
  1. Add the ip address that should be used for all migrations into the /etc/pve/datacenter.cfg file.

## 6. Format the HDD, SSD and NVME disks.
  1. Extend the data partition to 100% of the free space.
  1. Remove partitions from disks.
  1. Create new partitions, volume groups and logical volumes on the local disks.

# Created by: 

1. Luciano Sampaio.