
<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:1 -->

1. [Introduction](#1-introduction)
2. [URL](#2-url)
3. [Initial Setup](#3-initial-setup)
	1. [Domain](#i-domain)
	2. [Install](#ii-install)
4. [Setup Wizard](#4-setup-wizard)
5. [Adding Folder(s)](#5-adding-folders)

<!-- /TOC -->

## 1. Introduction

[Nextcloud](https://nextcloud.com) is a free, open-source, self-hosted file sharing solution, that functions similarly to Dropbox.

![](https://i.imgur.com/aIHp22i.png)

## 2. URL

 - To access Nextcloud, visit https://nextcloud._yourdomain.com_

## 3. Initial Setup

### i. Domain

- See [[Adding a Subdomain|Adding a Subdomain]] on how to add the subdomain `nextcloud` to your DNS provider.

- _Note: You can skip this step if you are using [[Cloudflare|Prerequisites: Cloudflare]] with Cloudbox._

### ii. Install

  - Run the following commands:

    ```bash
    cd ~/cloudbox/
    sudo ansible-playbook cloudbox.yml --tags nextcloud  
    ```

## 4. Setup Wizard

1. Visit https://nextcloud._yourdomain.com_

   ![](https://i.imgur.com/akcVDEl.png)

1. Under `Create an admin account`, set the following:

   - Username: fill in your preferred admin username.

   - Password: fill in your preferred admin password.

1. Click the `Storage & database` link.

   ![](https://i.imgur.com/BRpV7i6.png)

1. Under `data folder`, the path below should already be filled in.

   ```
   /data
   ```


3. Select `MySQL/MariaDB` under `Configure the database`.

   ![](https://i.imgur.com/Ck012rr.png)

4. Fill in the following **exactly** as you see below:

   - Database user: `root`

   - Database password: `password321` (The password is hard-coded in, so it cant be changed. But since the MariaDB container is closed to the outside, it's not an issue).

   - Database name: `nextcloud`

   - Database host: `mariadb:3306`

5. Click `Finish setup`.

   ![](https://i.imgur.com/jU8wOUD.png)

6. You will now be logged into Nextcloud.

## 5. Adding Folder(s)

1. Click the icon at the top right and select "Apps".

   ![](https://i.imgur.com/cHQUv1Z.png)

1. Enable `External storage support`. Type in your admin password to confirm.

   ![](https://i.imgur.com/2nKCBVt.png)

1. Click the icon at the top right and select "Settings".

   ![](https://i.imgur.com/c3vDcR7.png)

1. Click "External storages" under "Administration".

   ![](https://i.imgur.com/Gi7Lhxe.png)

1. For each folder you want to add, set the following:

   1. Folder name: your preference.

   1. External storage: `local`.

   1. Authentication: your preference (default is `None`).

   1. Configuration: `/mnt/unionfs/Media/path/to/folder` (make sure this path already exists; you could even share your entire `/mnt/unionfs/Media/` path).

   1. Available for: your preference (default is blank - for all users).

   1. Press the checkmark to save.

   ![](https://i.imgur.com/YCLJm5w.png)
