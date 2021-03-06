
<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:1 -->

1. [Intro](#1-intro)
2. [URL](#2-url)
3. [Initial Setup](#3-initial-setup)
	1. [Domain](#i-domain)
	2. [Install](#ii-install)
4. [Setup Wizard](#4-setup-wizard)
5. [Settings](#5-settings)

<!-- /TOC -->

## 1. Intro
[Plex Requests](http://plexrequests.8bits.ca/) is a simple automated way for users to request new content for Plex. 

![](https://i.imgur.com/mZELL2M.png)

![](https://i.imgur.com/XXAHC8k.png)

## 2. URL

- To access Plex Requests, visit https://plexrequests._yourdomain_.com

## 3. Initial Setup

### i. Domain

- See [[Adding a Subdomain|Adding a Subdomain]] on how to add the subdomain `plexrequests` to your DNS provider.

- _Note: You can skip this step if you are using [[Cloudflare|Prerequisites: Cloudflare]] with Cloudbox._

### ii. Install

  - Run the following commands:

    ```bash
    cd ~/cloudbox/
    sudo ansible-playbook cloudbox.yml --tags plexrequests  
    ```

## 4. Setup Wizard

1. First time you go to the Plex Requests page, you will be presented with the "Welcome to Plex Requests" screen. Click the orange-colored `admin page` link to be taken to the "Admin" page, then click the `Close` button.

    ![](https://i.imgur.com/nU4LllT.png)

1. You will see the "Sign in" prompt. Click the `Register` link at the bottom.

    ![](https://i.imgur.com/54U1EAA.png)

1. You will now see "Create an Account" prompt. Fill in your preferred `Email` and `Password` and click the `Register` button. This will be the Admin account for Plex Requests.

    ![](https://i.imgur.com/2axV0sW.png)

## 5. Settings

1. You will now be taken to the "General" settings page. You may select whatever options you like here. Click `Update Settings` to save changes.

    ![ ](https://i.imgur.com/02AlzFO.png)

1. On the "Authentication" settings page

    - It is advised to have both `Enable user authentication` and `Require users to login with their passwords` enabled (at the very least `Enable user authentication` enabled).

    - To have your Plex Authorization token automatically retrieved, fill in your `Plex Username` and `Plex Password` and click the `Get Token` button. When this is successful, you will get the "Successfully got token!" message and the `Plex authorization token` textbox will be filled in.

    - Click `Update Settings` to save changes.

    ![ ](https://i.imgur.com/vd35F5e.png)

    ![](https://i.imgur.com/gLucVsz.png)


1. On the "Radarr" settings page:

   _Note: There are some slight differences in the settings for Feeder / Plex setups. See notes below._ 


    - Check "Enable Radarr"

    - "Radarr server IP or Hostname": `radarr`

       - _For a Feeder / Plex setup, use `radarr.yourdomain.com` (or the IP address of your Feeder box) instead._


    - "Radarr server port":`7878`

       - _For a Feeder / Plex setup, use `443` instead._


    - "Radarr API key": [[Your Radarr API Key|Install: Radarr#9-retrieving-the-api-key]]


    - "Enable Radarr SSL": `disabled`.

       - _For Feeder / Plex setup, set it to `enabled`._


    - Click `Update Settings`.

    - Click `Test Radarr server`. The button will update to show "Success!".

    - Click `Get Profiles` and choose your preferred "Download quality profile for Radarr".

    - "Root save directory for movies": `/movies`.

    - Click `Update Settings`.

    ![](https://i.imgur.com/YKEPArN.png)

1. On the "Sonarr" settings page:

   _Note: There are some slight differences in the settings for Feeder / Plex setups. See notes below._ 

    - Check "Enable Sonarr"

    - "Sonarr server IP or Hostname": `sonarr`

       - _For Feeder / Plex setup, use `sonarr.yourdomain.com` (or the IP address of your Feeder box) instead._

    - "Sonarr server port":`8989`

       - _For Feeder / Plex setup, use `443` instead._

    - "Sonarr API key": [[Your Sonarr API Key|Install: Sonarr#9-retrieving-the-api-key]]

    - "Enable Sonarr SSL": `disabled`.

       - _For Feeder / Plex setup, set it to `enabled`._


    - Click `Update Settings`.

    - Click `Test Sonarr server`. The button will update to show "Success!".

    - Click `Get Profiles` and choose your preferred "Download quality profile".

    - "Root save directory for TV shows": `/tv`.

    - Click `Update Settings`.

    _Note: If you have a separate Plex and Feeder setup, this will be done on the server where Plex is installed.

    ![](https://i.imgur.com/fqnAyI5.png)

1. Click `Sign Out` to exit Settings.
