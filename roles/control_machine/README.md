# Setup the control machine to run Ansible scripts

Run the command in the terminal:
```bash
  01 - Add the unlock-keyring function into the ~/.bashrc file.
    nano ~/.bashrc
    # Function to unlock gnome keyring for headless logins.
    function unlock-keyring ()
    {
      read -rsp "Type your password: " pass
      export $(echo -n "$pass" | gnome-keyring-daemon --replace --unlock --daemonize)
      unset pass
    }

  02 - Run the unlock-keyring command on the terminal to unlock the secret - manager.
    source ~/.bashrc  
    unlock-keyring

  03 - Save your password in the secret manager.
    secret-tool store --label="local-user-password" password local-user-password

  04 - Run the playbook.
  ansible-playbook control_machine.yml
```

# Tasks:

## 1. Install required packages:  

## 2. Add passwords into the Secret Manager:
  1. *proxmox_root_password*. All the hosts will need to have the same root password in order to create the cluster.
  1. *proxmox_smtp_password*. The password that will be used to authenticate when sending email notifications.

# Created by: 

1. Luciano Sampaio.