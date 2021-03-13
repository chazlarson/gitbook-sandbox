## 1. Forward 

You will **NOT** use `root` to setup Cloudbox, as Cloudbox installs certain things to `/home/USER/` folder, where as, `root` uses `/root/` as it's home folder. This will definitely break the install.

Instead, you can use the guide below to create a non-root user account and use that going forward. 

**_TLDR: Do not use root to install Cloudbox._**

## 2. Setup


Choose **ONE** of the following:

###    i. Create a new user account `seed` (default)

- In this step, you will create the user account `seed` and add it to the `seed` and `sudo` groups.  

  _Note: Run the following commands line by line._

   ```bash
   sudo useradd -m seed
   sudo usermod -aG sudo seed
   sudo passwd seed
   sudo chsh -s /bin/bash seed
   su seed
   ```
 
_Note: If you have an existing user account that you don't plan on using, it may be a good idea to remove it and just stick with using `seed` for everything._

###    ii. Create new user account other than `seed`

- Run the following commands line by line:

   ```bash
   sudo useradd -m <username>
   sudo usermod -aG sudo <username>
   sudo passwd <username>
   sudo chsh -s /bin/bash <username>
   su <username>
   ```

- Set `user` in [[accounts.yml|Install: accounts.yml]] to your username.

_Note: If you decide to change your username after Cloudbox install, you will need to update the service.d files with your new username/group, see [[FAQ|FAQ#error-process-xxxxx-execstopbinfusermount--uz-mntplexdrive-codeexited-status217user]]._


###    iii. Use an existing (non-root) user account

- Run the following command: 


   ```bash
   sudo usermod -aG sudo <username>
   sudo usermod -aG <username> <username>
   ```

   _Note: This will set the group to the same name as your user account, which is required._


- Set `user` in [[accounts.yml|Install: accounts.yml]] to your username.

_Note: If you decide to change your username after Cloudbox install, you will need to update the service.d files with your new username/group, see [[FAQ|FAQ#error-process-xxxxx-execstopbinfusermount--uz-mntplexdrive-codeexited-status217user]]._


## 3. SSH Access

From now on, you will log into your server with the above account (**not** with root).

Example:
```bash
ssh user@serveripaddress
```

_Eventually, the server IP address can be replaced with cloudbox.domain.com (or mediabox.domain.com and feederbox.domain.com for Mediabox/Feederbox setups)._