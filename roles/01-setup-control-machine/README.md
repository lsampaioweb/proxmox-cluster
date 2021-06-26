# Setup control machine to run Ansible scripts

Run the command in the terminal:
```bash
  ansible-playbook 01-setup-control-machine.yml --ask-become-pass (or -K)
```

# Tasks:

## 1. Installing required packages:
  1. **SSH Pass**. It allows you to provide the ssh password without using the prompt. This will be necessary for the first settings when we don't have a SSH keypair yet.

# Created by: 

1. Luciano Sampaio.