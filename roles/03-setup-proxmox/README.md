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

# Created by: 

1. Luciano Sampaio.