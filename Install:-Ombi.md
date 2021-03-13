# work in progress - redoing parts of this page and simplifying steps


<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:0 orderedList:1 -->

1. [URL](#1-url)
1. [Initial Setup](#2-initial-setup)
1. [Settings](#3-settings)
   1. [Configuration](#i-configuration)
   1. [Media Server](#ii-media-server)
   1. [TV](#iii-tv)
   1. [Movies](#iii-movies)
   1. [Music](#iv-music)
1. [Plex Settings](#4-plex-settings)
1. [Radarr Settings](#5-radarr-settings)
1. [Sonarr Settings](#6-sonarr-settings)

<!-- /TOC -->
---
# 1. URL

 - To access Ombi, visit https://ombi._yourdomain_.com


# 2. Initial Setup

1. First time you go to the Ombi page, you will be presented with the "Welcome to Ombi" screen. Click the  **Next** button to continue.

   ![](https://i.imgur.com/w6r1vfP.png)

1. On the "Media Server Selection" page, select the media server of your choice (either **Emby** or **Plex**). Information on both setups are mentioned below. 

   ![](https://i.imgur.com/tbLysFM.png)


   _Note: You can skip this page if you want to set your preferred media server later._

   1. **Plex:**

      - Enter your Plex username and password and click the **Request Token** button.

        OR

      - Click **Continue With Plex** to login through Plex's site (_this doesn't work all the time_).


      ![](https://i.imgur.com/KLrjDTU.png)

   1. **Emby:**

      i. **Fill** in the following:

         - **Emby Hostname or IP Address**: `emby`

         - **Port**: `8096`

         - **Api Key**: [[Your Emby Api Key|Extras: Emby#6-api-key]]

      ii. Click the **Next** button to continue.

      ![](https://i.imgur.com/8nGz8OT.png)

5. Next screen will ask you to login to Ombi. Use the credentials from the previous screen to sign in (either the Plex account login or the Emby one). 

    ![](https://i.imgur.com/e7dkVAd.png)


# 3. Settings

Once logged in, click the **Settings** link at the top to be taken to the Settings page.

![](https://i.imgur.com/rrthXbP.png)

![](https://i.imgur.com/3kUc4iJ.png)


## i. Configuration


1. Select **Configuration** and then **Authentication**.

   ![](https://i.imgur.com/PNI5ywv.png)

   ![](https://i.imgur.com/E3ClVA5.png)


1. **Set** the following options:

   - **Allow users to login without a password**: `unchecked` (_your preference_)
   
   - **Enable Plex OAuth**: `checked` (_recommended_) 

   ![](https://i.imgur.com/P6kBXXi.png)

1. Click **Submit** to save.


##  ii. Media Server

### Plex

1. Select **Media Server** and then **Plex**.

   ![](https://i.imgur.com/kyr9O4g.png)

   ![](https://i.imgur.com/1kiDYnR.png)

1. **Fill** in the following settings:

   _Note: The loading of servers does not work, which is why we are doing the steps below._

   - **Server name**: `Plex` (_your preference_)
   
   - **Hostname or IP**: `plex`

   - **Port**: `32400`

   - **SSL**: `unchecked`

   - **Plex Authorization Token**: 'pre-filled' (_if not see [[Plex Access Token]]_)

   - **Machine Identifier**: Go to https://plex.yourdomain.com/identity and paste the `machineIdentifier` here.

1. Click the **Submit** button.

1. Now click the **Test Connectivity** button







Find the Media Server menu and select `Plex`.  Enter your Plex username and password, then his the `Load Servers` button.  This will scan for all of the Plex servers associated with the credentials you entered. Use the `Servers` button to hightlight the server you wish to configure Ombi with. While doing this will fill in the local hostname or IP section, it's best practice to use the dynamic name of `plex` in the Hostname field as seen in the image:

- ![](https://i.imgur.com/RUZW88d.png)

- Click the `Submit` button and then `Test Connectivity` button to verify Ombi is able to connect to your Plex instance.

### Emby

1. Select **Media Server** and then **Emby**.

   ![](https://i.imgur.com/kyr9O4g.png)

   ![](https://i.imgur.com/5jmdjqG.png)


##  iii. TV

##  iv. Movies



5. Radarr Settings

1. Under Movies menu section you will find the "Radarr" settings page:

   _Note: There are some slight differences in the settings for Feeder / Plex setups. See notes below._

   _Note: This is assuming you have already configured Radarr.  If Radarr has not been set up, some things below will not work; for example, Ombi can't get your Radarr root folders if you haven't set any up in Radarr yet._

    - Check "Enable Radarr"

    - "Radarr server IP or Hostname": `radarr`

       - _For a Feeder / Plex setup, use `radarr.yourdomain.com` (or the IP address of your Feeder box) instead._


    - "Radarr server port":`7878`

       - _For a Feeder / Plex setup, use `443` instead._


    - "Radarr API key": [[Your Radarr API Key|Install: Radarr#9-retrieving-the-api-key]]


    - "Enable Radarr SSL": `disabled`.

       - _For Feeder / Plex setup, set it to `enabled`._


    - Click `Submit`.

    - Click `Test Connectivity`. A fly in notification in the upper right corner will show "Successfully connected to Radarr!".

    - Click `Get Quality Profiles` and choose your preferred "Download quality profile for Radarr".

    - Click `Get Root Folders` and choose your preferred Root Folder, most cases it's simply `/Movies`.

    - Select the desired "Default Minimun Availability"

    - Click `Submit`.

     ![](https://i.imgur.com/J7MTPaz.png)

6. Sonarr Settings

1. Under TV menu section you will find the "Sonarr" settings page:

   _Note: There are some slight differences in the settings for Feeder / Plex setups. See notes below._

   _Note: This is assuming you have already configured Sonarr.  If Sonarr has not been set up, some things below will not work; for example, Ombi can't get your Sonarr root folders if you haven't set any up in Sonarr yet._

    - Check "Enable Sonarr"

    - "Sonarr server IP or Hostname": `sonarr`

       - _For Feeder / Plex setup, use `sonarr.yourdomain.com` (or the IP address of your Feeder box) instead._

    - "Sonarr server port":`8989`

       - _For Feeder / Plex setup, use `443` instead._

    - "Sonarr API key": [[Your Sonarr API Key|Install: Sonarr#9-retrieving-the-api-key]]

    - "Enable Sonarr SSL": `disabled`.

       - _For Feeder / Plex setup, set it to `enabled`._


    - Click `Submit`.

    - Click `Test Connectivity`. A fly in notification in the upper right corner will show "Successfully connected to Sonarr!".

    - Click `Get Quality Profiles` and choose your preferred "Download quality profile".

    - Click `Get Root Folders` and choose your preferred Root Folder, most cases it's `/tv` for TV shows.

    - Enable season folders if you wish.

    - Click `Submit`.

    _Note: If you have a separate Plex and Feeder setup, this will be done on the server where Plex is installed.

    ![](https://i.imgur.com/HXYBT5K.png)
