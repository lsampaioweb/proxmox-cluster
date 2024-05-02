# Setup Proxmox

Run the command in the terminal:
```bash
# The default inventory is "home".
ansible-playbook proxmox.yml
ansible-playbook proxmox.yml -i "inventory/home"
ansible-playbook proxmox.yml -i "inventory/homelab"
```

#
### Tasks:

### 1. Setup email notification with Postfix.
  1. Add the SMTP server, user name and password into the sasl_passwd file.
  1. Add relayhost into the main.cf file.
  1. Add SASL authentication into the main.cf file.

### 2. Remove the no subscription popup.
  1. Replace the verification with a if (false).

### 3. Create the cluster and join the nodes into it.
  1. Create the cluster.
  1. Add nodes to the cluster.
  1. Add the fingerprint of each host into the ~/.ssh/known_hosts file:
  ```bash
    pve-01.homelab ecdsa-sha2-nistp256 ...
    pve-02.homelab ecdsa-sha2-nistp256 ...
    pve-03.homelab ecdsa-sha2-nistp256 ...
    pve-04.homelab ecdsa-sha2-nistp256 ...
    pve-05.homelab ecdsa-sha2-nistp256 ...
    pve-06.homelab ecdsa-sha2-nistp256 ...
    pve-07.homelab ecdsa-sha2-nistp256 ...
  ```

### 4. Set the network for all migrations in the cluster.
  1. Add the ip address that should be used for all migrations into the /etc/pve/datacenter.cfg file.

### 5. Format the HDD, SSD and NVME disks.
  1. Extend the data partition to 100% of the free space.
  1. Remove partitions from disks.
  1. Create new partitions, volume groups and logical volumes on the local disks.

### 6. Create the resource pools.
  1. Template, Staging and Production.

### 7. Create the Roles.
  1. Packer.

#
### Created by:

1. Luciano Sampaio.