# Setup Proxmox

Run the command in the terminal:
```bash
  ansible-playbook 03-setup-proxmox.yml
```

# Tasks:

## 1. Add the internal IP and url of all hosts into the 'hosts' file.
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
    host01.aprendendo.com.br ecdsa-sha2-nistp256 ...
    host02.aprendendo.com.br ecdsa-sha2-nistp256 ...
    host03.aprendendo.com.br ecdsa-sha2-nistp256 ...
  ```

## 5. Set the network for all migrations in the cluster.
  1. Add the ip address that should be used for all migrations into the /etc/pve/datacenter.cfg file.


# Created by: 

1. Luciano Sampaio.