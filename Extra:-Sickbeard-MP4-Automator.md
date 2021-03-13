<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:0 orderedList:1 -->

1. [Introduction](#1-introduction)
2. [Overview](#2-overview)
3. [Initial Setup](#3-initial-setup)
	1. [Settings](#i-settings)
	2. [Install](#ii-install)
4. [Setup](#4-setup)
5. [Sonarr](#5-sonarr)
6. [Radarr](#6-radarr)
7. [Tips](#7-tips)
8. [User Submitted Configs](#8-user-submitted-configs)

<!-- /TOC -->

## 1. Introduction

[Sickbeard MP4 Automator](https://github.com/mdhiggins/sickbeard_mp4_automator) Automatically converts video files to a standardized mp4 format.


## 2. Overview

1. Download is handed back to Sonarr/Radarr from NZBGet/ruTorrent.

1. Sonarr/Radarr renames the file and executes the Sickbeard MP4 Automator (SMA) script.

1. SMA runs, converts the renamed file to an mp4, following the config in `autoProcess.ini`, and deletes the original file (can be changed in the settings). 

1. SMA executes the `plex_autoscan.py` post-processing script to notify Plex Autoscan to scan the new file's directory.

1. SMA notifies Sonarr/Radarr of the new filename and initiates a rescan of the file location to pick up the change.

## 3. Initial Setup

Sickbeard MP4 Automator is installed on 'Cloudbox' or 'Feederbox' setups.


### i. Settings

Set the following option in `adv_settings.yml`:

```yaml
sickbeard_mp4_automator: yes
```

### ii. Install

Run the following command:

```bash
sudo ansible-playbook cloudbox.yml --tags sickbeard_mp4_automator
```

or

```bash
sudo ansible-playbook cloudbox.yml --tags sma
```

## 4. Setup

### i. Add your Plex Autoscan URL into 'plex_autoscan.py'

On a full 'Cloudbox' install, the `URL=` should be set to your [[Plex Autoscan URL|Install: Plex-Autoscan#3-obtaining-the-plex-autoscan-url]] on line 32 of `/opt/scripts/sickbeard_mp4_automator/post_process/plex_autoscan.py`.

If not, or if your are using a 'Feederbox' setup, replace `PLEX_AUTOSCAN_URL` with your [[Plex Autoscan URL|Install: Plex-Autoscan#3-obtaining-the-plex-autoscan-url]].

```python
url = "PLEX_AUTOSCAN_URL"
```

### ii. Fill in API Keys into 'autoProcess.ini'

Out of box, the install process would have put your Sonarr and Radarr API keys into `/opt/scripts/sickbeard_mp4_automator/autoProcess.ini`.

If they are missing, you will need to add them in yourself.


## 5. Sonarr

### i. Set 'Plex Autoscan' to rename only

_This is now handled by the 'plex\_autoscan.py' script._

1. Click "Settings" -> "Connect".

1. Click 'Plex Autoscan'.

1. Set the following (in order):

   1. Name: Plex Autoscan

   1. On Grab: `No`

   1. On Download: `Yes`

   1. On Upgrade: `No`

   1. On Rename: `Yes`

   1. On Download: `No` (this is not a typo)

1. Click "Save"

1. The box will look like this:

   ![](https://i.imgur.com/aa1nt0Z.png)


### ii. Add 'Sickbeard MP4 Automator'

1. Click "Settings" -> "Connect".

1. Add a new "Custom Script".

1. Add the following:

   1. Name: Sickbeard MP4 Automator

   1. On Grab: `No`

   1. On Download: `Yes`

   1. On Upgrade:  `Yes`

   1. On Rename: `No`

   1. Path: `/scripts/sickbeard_mp4_automator/postSonarr.py`

   1. Arguments: (blank)

1. The settings will look like this:

   ![SMA for Sonarr](https://i.imgur.com/G5wVtC8.png)

1. Click "Save" to add the Sickbeard MP4 Automator script.


## 6. Radarr

### i. Set 'Plex Autoscan' to rename only

_This is now handled by the 'plex\_autoscan.py' script._

1. Click "Settings" -> "Connect".

1. Click 'Plex Autoscan'.

1. Set the following (in order):

   1. Name: Plex Autoscan

   1. On Grab: `No`

   1. On Download: `Yes`

   1. On Upgrade: `No`

   1. On Rename: `Yes`

   1. On Download: `No` (this is not a typo)

1. Click "Save"

1. The box will look like this:

   ![](https://i.imgur.com/aa1nt0Z.png)



### ii. Add 'Sickbeard MP4 Automator'

1. Click "Settings" -> "Connect".

1. Add a new "Custom Script".

1. Add the following:

   1. Name: Sickbeard MP4 Automator

   1. On Grab: `No`

   1. On Download: `Yes`

   1. On Upgrade:  `Yes`

   1. On Rename: `No`

   1. Path: `/scripts/sickbeard_mp4_automator/postRadarr.py`

   1. Arguments: (blank)

1. The settings will look like this:

   ![SMA for Radarr](https://i.imgur.com/q6bjG3x.png)

1. Click "Save" to add the Sickbeard MP4 Automator script.

## 7. Tips

### Enable HW acceleration for supported Intel CPUs

Set the following in `/opt/scripts/sickbeard_mp4_automator/autoProcess.ini`: 
 
```ini
use-qsv-decoder-with-encoder = True
```

```ini
video-codec = h264vaapi, h264, x264
```

Set the next one only if your server's CPU is capable of HW decoding HEVC. See [here](https://en.wikipedia.org/wiki/Intel_Quick_Sync_Video#Hardware_decoding_and_encoding).

```ini
use-hevc-qsv-decoder = True
```


## 8. User Submitted Configs

- [[Kinv|SMA Config by kinv]]