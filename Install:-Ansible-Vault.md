[[Ansible Vault|https://docs.ansible.com/ansible/2.6/user_guide/vault.html]] is a feature of Ansible that allows users to encrypt data with AES 256 cipher. This allows us to secure sensitive data, such as passwords and keys, and have Ansible decrypt them automatically when they are needed.

We will use this to encrypt [[accounts.yml|Install: accounts.yml]], where all the account info is stored.

This is an optional step; you do not have to set this up as part of the install.  **If you do set it up, make sure you keep track of the password, as this password file is not backed up by the built-in backup**.

_Note: For more information on Ansible Vault, checkout the [[Ansible Vault Primer]]._

##

## 1. Set Nano As Your Current Editor 


```
export EDITOR=nano
```

_Note: This is only needed for new installs as Cloudbox installer will set nano to be the default editor._


## 2. Create a Password File

1. First we need to create a password file. 

   ```
   nano ~/.ansible_vault
   ```

1. Type in a password.  This does not have to be [and should not be] your user or root password.  It is used solely for securing this ansible accounts file:

   ```
   yourpassword
   ```

1. When done editing, save the file: <kbd class="platform-all">Ctrl + X</kbd> <kbd class="platform-all">Y</kbd> <kbd class="platform-all">Enter</kbd>.

## 3. Edit Ansible Config

We will now need to add the location of the password file into `ansible.cfg`, in the format of:

1. Edit `ansible.cfg`:

   ```
   nano ~/cloudbox/ansible.cfg
   ```

1. Add the following line:

   ```
   vault_password_file = $HOME/.ansible_vault
   ```

1. It should now look like this:

   ```
   [defaults]
   inventory = inventories/local
   callback_whitelist = profile_tasks
   command_warnings = False
   retry_files_enabled = False
   hash_behaviour = merge
   vault_password_file = $HOME/.ansible_vault
   ```

1. When done editing, save the file: <kbd class="platform-all">Ctrl + X</kbd> <kbd class="platform-all">Y</kbd> <kbd class="platform-all">Enter</kbd>.

## 4. Encrypt `accounts.yml`

1. Run the following command:

   ```
   ansible-vault encrypt ~/cloudbox/accounts.yml
   ```

1. You will get the following output:

   ```
   Encryption successful
   ```

Remember: **This password file is not backed up by the built-in backup; make a backup of it now, or save the password in a secure place.**