# Setup Proxmox

Run the command in the terminal:
```bash
  ansible-playbook 03-setup-proxmox.yml
```

# Tasks:

## 1. Add the internal IP and url of all hosts into the 'hosts' file.
  1. Add the internal IP and url of all hosts into the 'hosts' file.

## 2. Add the fingerprint of each host into the ~/.ssh/known_hosts file:
    host01.aprendendo.com.br,host01,192.168.0.31 ecdsa-sha2-nistp256 ...
    host02.aprendendo.com.br,host02,192.168.0.32 ecdsa-sha2-nistp256 ...
    host03.aprendendo.com.br,host03,192.168.0.33 ecdsa-sha2-nistp256 ...

## 3. Setup email notification with Postfix.
  1. Add the SMTP server, user name and password into the sasl_passwd file.
  1. Add relayhost into the main.cf file.
  1. Add SASL authentication into the main.cf file.

## 4. Remove the no subscription popup.
  1. Replace the verification with a if (false).

## 5. Create the cluster and join the nodes into it.
  1. Create the cluster.
  1. Add nodes to the cluster.

# Created by: 

1. Luciano Sampaio.