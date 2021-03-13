[Plex Autoscan](https://github.com/l3uddz/plex_autoscan/) (by [l3uddz](https://github.com/l3uddz/)) is a script that assists Plex with the adding media files, that were imported by Sonarr / Radarr, by only scanning the folder that has been imported (vs the entire section library folder), thereby preventing Google API bans.

Plex Autoscan comes configured out of the box (as related to Cloudbox). However, there a few things that need to be set by you.

_If you would like to learn more about what Plex Autoscan does and all the options available, visit https://github.com/l3uddz/plex_autoscan._


## 1. Do a One-Time, Manual Scan in Plex

 - For Plex Autoscan to work, at least one item needs to exist in each library before new items can show up. 

 - If you already have media, simply add it to the library and do a manual scan within Plex, for each library you have, to build the DB.  

 - If you currently don’t have any media, continue on with the setup, and when you have acquired some media, you will then perform a do a manual scan within Plex, for each library, to build the DB.  

 - For more info, see [[this|Install: Plex-Media-Server#5-scan-media-libraries]]. 

## 2. Add Your Plex Access Token into Plex Autoscan Config

_You can skip this step if you entered in your Plex credentials in [[accounts.yml|Install: accounts.yml]] during setup._

_Note: For Mediabox / Feederbox setups, the following will be done on the Mediabox._

 
   1. Get your Plex Autoscan Token [[here|Plex Access Token]].

   1. On the server's shell, run the following command:

      ```
      nano /opt/plex_autoscan/config/config.json
      ```
   1. Add the Plex Access Token to `"PLEX_TOKEN":` so that it now appears as:

      ```
      "PLEX_TOKEN": "xxxxxxxxxxxxxx",
      ```

      Note: Make sure it is within the quotes (`"`) and there is a comma (`,`) after it.

   1. <kbd class="platform-all">Ctrl + X</kbd> <kbd class="platform-all">Y</kbd> <kbd class="platform-all">Enter</kbd> to save.

## 3. Obtaining the Plex Autoscan URL

_Note: For Mediabox / Feederbox setup, the following will be done on the Mediabox._

The Plex Autoscan URL is needed during the setup of [[Sonarr|Install: Sonarr#plex-autoscan]], [[Radarr|Install: Radarr#plex-autoscan]], and [[Lidarr|Install: Lidarr#plex-autoscan]].


To get your Plex Autoscan URL, run the following command:

 ```shell
 /opt/scripts/plex_autoscan/plex_autoscan_url.sh
 ```

This will be in the format of:

```
http://subdomain.domain.com:plex_autoscan_port/plex_autoscan_pass
```
or
```
http://server_ip_address:plex_autoscan_port/plex_autoscan_pass
```

Example:
```
http://plex.domain.com:3468/aiG7Uwie9iodTTlaisahcieNaeVonu6I
```

_Note 1: The url will not use _plex.domain.com_ if the IP address it points to does not match the server's IP address (e.g. Cloudflare CDN enabled)._ 

_Note 2: If the url is _plex.domain.com_, but you decide to enable Cloudflare proxy for the `plex` subdomain later, you will need to generate another Plex Autoscan URL and add that into Sonarr/Radarr/Lidarr instead, as the scan request will need to go to you server's actual IP and not a Cloudflare one._

_Note 3: For Mediabox setups, make sure that the port is open in the firewall and/or router._

_Note 4: The PAS URL is not meant to be accessed via a browser by default (i.e. going there will give you a `401 Unauthorized` error). However, you can enable a web UI for manual scan requests, see [here](https://github.com/Cloudbox/Cloudbox/wiki/Plex-Autoscan-Extras#web-app)._

## 4. Upload Control File to Google Drive

The following step is important so that Plex Autoscan can remove missing/replaced media files out of Plex (i.e. empty trash). Without it, Plex will be left with "unavailable" media that can't play (i.e. media posters with trash icons on them).

For more details on what the control file is, see [[here|FAQ#purpose-of-a-control-file-in-plex-autoscan]].

To upload the mounted.bin control file, run the following command:

```
rclone touch google:/mounted.bin
```

_Note 1: If your Rclone remote config has a different name for Google Drive, replace `google:` with yours'._

_Note 2: Above command requires Rclone version 1.39+_

_Note 3: If you use different mount paths for your libraries in Plex this change must also be reflected in the config.json in SERVER_PATH_MAPPINGS_
Example:
```  "SERVER_PATH_MAPPINGS": {
    "/mnt/unionfs/Media/Movies/": [
      "/movies/",
      "/mnt/unionfs/Media/Movies/",
      "My Drive/Media/Movies/"
    ],
```