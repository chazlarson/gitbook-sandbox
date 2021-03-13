<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:1 -->

1. [Introduction](#1-introduction)
2. [URL](#2-url)
3. [Initial Setup](#3-initial-setup)
	1. [Domain](#i-domain)
	2. [Install](#ii-install)
4. [Setup Wizard](#4-setup-wizard)
5. [Adding Folder(s)](#5-adding-folders)

<!-- /TOC -->

---

## 1. Introduction

[Resilio Sync](https://www.resilio.com/individuals/) (formerly BitTorrent Sync) by Resilio, Inc. is a proprietary peer-to-peer file synchronization tool available for Windows, Mac, Linux, Android, iOS, Windows Phone, Amazon Kindle Fire and BSD. It can sync files between devices on a local network, or between remote devices over the Internet via a modified version of the BitTorrent protocol. 

-Wikipedia

![](https://camo.githubusercontent.com/745c768935c59dcf6430437cf2fd000144bc4fd8/68747470733a2f2f692e696d6775722e636f6d2f74356c725650342e706e67)

## 2. URL

 - To access Resilio Sync, visit http://resiliosync._yourdomain.com_

## 3. Initial Setup

### i. Domain

- See [[Adding a Subdomain|Adding a Subdomain]] on how to add the subdomain `resiliosync` to your DNS provider.

- _Note: You can skip this step if you are using [[Cloudflare|Prerequisites: Cloudflare]] with Cloudbox._

### ii. Install

- Run the following commands:

  ```bash
  cd ~/cloudbox/
  sudo ansible-playbook cloudbox.yml --tags resilio-sync
  ```

## 4. Setup Wizard

1. Visit https://resiliosync._yourdomain.com_

1. First time you log in, you will be presented with a welcome screen.

1. Fill in the following:

   - User name: fill in your preferred admin username.

   - Password: fill in your preferred admin password.

   - Confirm password: retype the password.

1. Click "Continue".

   ![](https://i.imgur.com/klEIhGQ.png)

1. Next screen will ask to choose a product. This will be "Sync Home" for most users. Click the product that applies to you.

   _For this guide, we will select "Sync Home"._

   ![](https://i.imgur.com/vZ0vG4m.png)

1. Next screen will ask for a "friendly" name for your Resilio Sync server. Type in a name and check the boxes  below. Click "Get Started" to continue.

   ![](https://i.imgur.com/glH7nL1.png)

1. You will be asked to login with the username and password you setup earlier.

   ![](https://i.imgur.com/SRFQNEP.png)


## 5. Adding Folder(s)

1. Click the `+` at the top left and select the folder type.

   _For this guide, we will select "Standard folder"._

   ![](https://i.imgur.com/HS3ENBc.png)

1. On the next screen, click `mounted_folders` to expand it

   _Note: Do not use the `sync` folder (`/mnt/sync/` path) as this folder will only be used to save config files._

   ![](https://i.imgur.com/FUI8hA8.png)

   ![](https://i.imgur.com/ewuZ31k.png)

1. The `home` and `mnt` folders under `mounted_folders` represent the folders `home` and `mnt` on your server's `/` path.

   So..

   - Resilio Sync: `/mnt/mounted_folders/home/` = Server: `/home/`

   - Resilio Sync: `/mnt/mounted_folders/mnt/` = Server: `/mnt/`

1. You can either choose an existing folder to share or you can create a new folder. When you are ready to share, click "Open".

   _For this guide, we will created the following folder on our server: `/home/seed/test/` (`/mnt/mounted_folders/home/seed/test/` within Resilio Sync)._


1. On the next screen, select the sharing options (e.g. "Read Only" or "Read & Write", link expiration, etc). You can share this folder via a Link, Key, and/or QR Code. When you're done, click the `x` at the top right.

   ![](https://i.imgur.com/nIP6HoJ.png)

1. You will now see the folder being shared.

   ![](https://i.imgur.com/t5lrVP4.png)
