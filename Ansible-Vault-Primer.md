This page is a primer on Ansible Vault and, as an example, it will take you through encrypting your [[accounts.yml|Install: accounts.yml]] file as well.



# Introduction

Ansible Vault is a feature of Ansible that allows users to encrypt data with AES 256 cipher. This allows us to secure sensitive data, such as passwords and keys, and have Ansible decrypt them automatically when they are needed.

When an Ansible Playbook is run the encrypted data is decrypted on the fly via a user-supplied password. This password is either provided via a password file or with a prompt.

# Ansible Vault Basics

## Encrypting a File

To encrypt `accounts.yml`, follow these steps.

1. Go to the Cloudbox folder:

   ```bash
   cd ~/cloudbox/
   ```

1. Run the following command:

   ```
   ansible-vault encrypt accounts.yml
   ```

1. Set a new password at the prompt and confirm:

   ```
   New Vault password:
   Confirm New Vault password:
   ```

1. When finished, you'll get this: 

   ```
   Encryption successful
   ```

1. The `accounts.yml` file will now look like this:

   ```
   $ANSIBLE_VAULT;1.1;AES256
   38393264656134313831626566383335336438363265363163323736653834616537303030666537
   3561666539363138663162303633323264643665333938390a616638636531306439383034346166
   30656535656564366665333637633935656564393633636432613064373832373663313765653635
   3339666361393166340a316566386134376235366465626337313665353565323237376338633064
   32333838396136373038643963373932353632613033366665613836316336633538633737323466
   34653461323636626638613264643334613763623365626339616636646537343339383537323464
   64336331623665373362393435313730383831303163316161343664613731346139633737363264
   30396366636332663032633438376136613831663862313437633130656636353633323264643839
   36353665313231653564616636313931646538323965383539313931636164393861326635306235
   65623030393166343635346437633638393161363962363439336138613437336231353430323762
   38306435616535343737396438663930393933346434306139633538653861613633346536326663
   32373634383839653665
   ```


## Viewing an Encrypted File

To view the contents of `accounts.yml`, follow these steps.

_Note: The decryption only lasts while it is open on the screen, and until you hit the <kbd class="platform-all">Q</kbd> key._

1. Go to the Cloudbox folder:

   ```bash
   cd ~/cloudbox/
   ```

1. Run the following command:

   ```
   ansible-vault view accounts.yml
   ```

1. Type in the password at the prompt:

   ```
   Vault password:
   ```

1. The screen will now show you the contents:

   ```
   ---
   user: seed
   passwd: password123
   domain: testcloudbox.ml
   email: your@email.com
   cloudflare_api_token:
   (END)
   ```

1. When finished viewing, hit <kbd class="platform-all">Q</kbd>.


## Editing an Encrypted File

To edit the contents of `accounts.yml`, follow these steps.

1. Go to the Cloudbox folder:

   ```bash
   cd ~/cloudbox/
   ```

1. Run the following command:

   ```
   ansible-vault edit accounts.yml
   ```

1. Type in the password at the prompt:

   ```
   Vault password:
   ```

1. This will open the decrypted file in nano.


1. When done editing, save the file: <kbd class="platform-all">Ctrl + X</kbd> <kbd class="platform-all">Y</kbd> <kbd class="platform-all">Enter</kbd>.

## Changing the Password of an Encrypted File

To change the password of `accounts.yml`, follow these steps.

1. Go to the Cloudbox folder:

   ```bash
   cd ~/cloudbox/
   ```

1. Run the following command:

   ```
   ansible-vault rekey accounts.yml
   ```

1. Type in the current password at the prompt:

   ```
   Vault password:
   ```

1. Type in and confirm a new vault password:

   ```
   New Vault password:
   Confirm New Vault password:
   ```

1. After successful re-encryption, you'll see this:

   ```
   Rekey successful
   ```

## Decrypting an Encrypted File

To decrypt `accounts.yml`, follow these steps.

_Note: The decryption here is permanent, until you re-encrypt the file again._

1. Go to the Cloudbox folder:

   ```bash
   cd ~/cloudbox/
   ```

1. Run the following command:

   ```
   ansible-vault decrypt accounts.yml
   ```

1. Type in the password at the prompt:

   ```
   Vault password:
   ```

1. When finished, you'll get this: 

   ```
   Decryption successful
   ```


1. `settings.yml` will now look like this:

   ```
   ---
   user: seed
   passwd: password123
   domain: testcloudbox.ml
   email: your@email.com
   cloudflare_api_token:
   ```



# Password File Setup

Storing the password in a password file allows Ansible to run commands without a prompt. 

The following commands can run without password prompts:

- `ansible-vault view`
- `ansible-vault edit`
- `ansible-vault encrypt`
- `ansible-vault decrypt`

Once a password file is created, it's location will need to be added to `ansible.cfg`. 

_Note: Prompted vault passwords (i.e. `--ask-vault-pass` or `--vault-id @prompt`) will not work with Cloudbox's Ansible playbook, however, you can use some other scripted solution (e.g. ssh based key script with ssh forwarding) to generate a password file and pass the path location to the env variable `ANSIBLE_VAULT_PASSWORD_FILE`._


## Password File

1. First we need to create a password file. The location and name is up to you.

   ```
   touch ~/.ansible_vault 
   ```

1. Will use an example password of `password321`.

   ```
   nano ~/.ansible_vault
   ```

1. Type in your password

   ```
   password321
   ```

1. When done editing, save the file: <kbd class="platform-all">Ctrl + X</kbd> <kbd class="platform-all">Y</kbd> <kbd class="platform-all">Enter</kbd>.

1. The password file will look like this: 

   Command:
   ```
   cat ~/.ansible_vault
   ```

   Output:
   ```
   password321
   ```

## Ansible Config

We will now need to add the location of the password file into `ansible.cfg`, in the format of:

```
vault_password_file = /PATH/TO/PASSWORD/FILE
```

Example:

Command:
```
cd ~/cloudbox
cat ansible.cfg
```

Output:
```
[defaults]
inventory = inventories/local
callback_whitelist = profile_tasks
command_warnings = False
retry_files_enabled = False
hash_behaviour = merge
vault_password_file = ~/.ansible_vault
```


## Encrypt Settings

If you haven't already done so, encrypt the `accounts.yml` file. You will not be prompted for a password this time.

Command:
```
ansible-vault encrypt accounts.yml
```

Output:
```
Encryption successful
```

## Ansible Playbook

Running `ansible-playbook` tasks, will no longer prompt you for a vault password. 

Each time a playbook is ran, the decryption will occur on-the-fly, but will remain encrypted after the playbook finishes. 

Example:

```
sudo ansible-playbook cloudbox.yml --tags cloudbox
```


