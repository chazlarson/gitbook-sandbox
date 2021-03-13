_Last updated on Feb 10, 2020._

## Basics ##
1. [[Introduction|Basics: Introduction]]
1. [[Cloudbox Install Types|Basics: Cloudbox Install Types]]
1. [[Cloudbox Paths|Basics: Cloudbox Paths]]
1. [[Accessing Cloudbox Apps|Basics: Accessing Cloudbox Apps]]


## Prerequisites ##
1. [[Overview|Prerequisites: Overview]]
1. [[Presumptions|Prerequisites: Presumptions]]
1. [[Server|Prerequisites: Server]]
1. [[Domain Name|Prerequisites: Domain Name]]
1. [[Cloudflare|Prerequisites: Cloudflare]] (Optional, but recommended)
1. [[Cloud Storage|Prerequisites: Cloud Storage]]
1. [[Plex|Prerequisites: Plex]] / [[Emby|Prerequisites: Emby]] - Account
1. [[Usenet vs. BitTorrent|Prerequisites: Usenet vs BitTorrent]]


## Install Cloudbox ##


<details open><summary><strong>Cloudbox</strong></summary>

1. [[Overview|Install: Overview]]
1. [[Dependencies|Install: Dependencies]] (Choose only one of these)
   - [[Master Branch (default)|Install: Dependencies (Master Branch)]]
   - [[Develop Branch|Install: Dependencies (Develop Branch)]]
1. [[Ansible Vault|Install: Ansible Vault]]
1. [[Settings|Install: Settings]]
   - [[accounts.yml|Install: accounts.yml]]
   - [[settings.yml|Install: settings.yml]]
1. [[Preinstall|Install: Preinstall]] (Choose only one of these)
   - [[Master Branch (default)|Install: Preinstall (Master Branch)]]
   - [[Develop Branch|Install: Preinstall (Develop Branch)]]
1. [[SSH|Install: SSH]]
1. [[Rclone|Install: Rclone|Install: Rclone]]
1. [[Cloudbox|Install: Cloudbox]] (Choose only one of these)
   - [[Master Branch (default)|Install: Cloudbox (Master branch)]]
   - [[Develop Branch|Install: Cloudbox (Develop branch)]]
1. Application Setup
    1. [[NZBGet|Install: NZBGet]]
    1. [[ruTorrent|Install: ruTorrent]]
    1. [[NZBHydra2|Install: NZBHydra2]]
    1. [[Jackett|Install: Jackett]]
    1. [[Plex Media Server|Install: Plex Media Server]]
    1. [[Plex Autoscan|Install: Plex Autoscan]]
    1. [[Sonarr|Install: Sonarr]]
    1. [[Radarr|Install: Radarr]]
    1. [[Lidarr|Install: Lidarr]]
    1. [[PlexPy (Tautulli)|Install: PlexPy (Tautulli)]]
    1. [[Ombi|Install: Ombi]]
    1. [[Portainer|Install: Portainer]]
    1. [[Organizr|Install: Organizr]]
</details>

<br />


## Install Feederbox / Mediabox  ##

<details open><summary><strong>Feederbox</strong> (do this first)</summary>

1. [[Overview|Install: Overview]]
1. [[Dependencies|Install: Dependencies]]
   - [[Master Branch (default)|Install: Dependencies (Master Branch)]]
   - [[Develop Branch|Install: Dependencies (Develop Branch)]]
1. [[Ansible Vault|Install: Ansible Vault]]
1. [[Settings|Install: Settings]]
   - [[accounts.yml|Install: accounts.yml]]
   - [[settings.yml|Install: settings.yml]]
1. [[Preinstall|Install: Preinstall]] (Choose only one of these)
   - [[Master Branch (default)|Install: Preinstall (Master Branch)]]
   - [[Develop Branch|Install: Preinstall (Develop Branch)]]
1. [[SSH|Install: SSH]]
1. [[Rclone|Install: Rclone|Install: Rclone]]
1. [[Feederbox|Install: Feederbox]] (Choose only one of these)
   - [[Master Branch (default)|Install: Feederbox (Master branch)]]
   - [[Develop Branch|Install: Feederbox (Develop branch)]]
1. Application Setup
    1. [[NZBGet|Install: NZBGet]]
    1. [[ruTorrent|Install: ruTorrent]]
    1. [[NZBHydra2|Install: NZBHydra2]]
    1. [[Jackett|Install: Jackett]]
    1. [[Sonarr|Install: Sonarr]]
    1. [[Radarr|Install: Radarr]]
    1. [[Lidarr|Install: Lidarr]]
    1. [[Portainer|Install: Portainer]]
    1. [[Organizr|Install: Organizr]]

</details>

<br />

<details open><summary><strong>Mediabox</strong></summary>

1. [[Overview|Install: Overview]]
1. [[Dependencies|Install: Dependencies]]
   - [[Master Branch (default)|Install: Dependencies (Master Branch)]]
   - [[Develop Branch|Install: Dependencies (Develop Branch)]]
1. [[Ansible Vault|Install: Ansible Vault]]
1. [[Settings|Install: Settings]]
   - [[accounts.yml|Install: accounts.yml]]
   - [[settings.yml|Install: settings.yml]]
1. [[Preinstall|Install: Preinstall]] (Choose only one of these)
   - [[Master Branch (default)|Install: Preinstall (Master Branch)]]
   - [[Develop Branch|Install: Preinstall (Develop Branch)]]
1. [[SSH|Install: SSH]]
1. [[Rclone|Install: Rclone|Install: Rclone]]
1. [[Mediabox|Install: Mediabox]] (Choose only one of these)
   - [[Master Branch (default)|Install: Mediabox (Master branch)]]
   - [[Develop Branch|Install: Mediabox (Develop branch)]]
1. Application Setup
    1. [[Feeder Mount]]
    1. [[Plex Media Server|Install: Plex Media Server]]
    1. [[Plex Autoscan|Install: Plex Autoscan]]
    1. [[PlexPy (Tautulli)|Install: PlexPy (Tautulli)]]
    1. [[Ombi|Install: Ombi]]

</details>

## Recommended Reading ##
- [[Cloudplow]] (Media Uploader)
- [[Updating Cloudbox]]
- [[Updating Cloudbox Apps]]
- [[Migrating Cloudbox]]
- [[Settings Updater]]

## Backup and Restore  ##
- [[ Backup and Restore | Cloudbox Backup and Restore]]
- [[ Settings | Cloudbox Backup and Restore Settings]]
- [[ Scheduling | Cloudbox Backup and Restore Scheduling]]
- [[Migrating Cloudbox]]
- [[FAQ | https://github.com/Cloudbox/Cloudbox/wiki/FAQ#cloudbox-backup-and-restore]]
  - [[What is backed up? | https://github.com/Cloudbox/Cloudbox/wiki/FAQ#what-is-backed-up]]
  - [[What is Cloudbox Restore Service? | https://github.com/Cloudbox/Cloudbox/wiki/FAQ#what-is-cloudbox-restore-service]]


## More Information ##
- [[Ansible Vault Primer]]
- [[Plex Access Token]]
- [[Plex Autoscan Extras]]
- [[Pushover]]
- [[Google Drive API Client ID and Client Secret]]
- [[Useful Docker Commands]]
- [[Add Your Own Docker Container into Cloudbox]]
- [[Revoking SSL Certificates]]
- [[Feeder Mount]]
- [[Adding a Subdomain|Adding a Subdomain]]
- [[HTTP Auth Support|HTTP Auth Support]]

## Advanced Configuration ##
- [[Customizing Plex Libraries]]
- [[adv_settings.yml|adv_settings.yml]]

## Experimental ##
- [[Downloading into the unionfs mount]]

## Extras ##
- [[Emby|Extras: Emby]]
- [[Nextcloud|Extras: Nextcloud]]
- [[Resilio Sync|Extras: Resilio Sync]]
- [[Plex DupeFinder|Extras: Plex DupeFinder]]
- [[Heimdall|Extras: Heimdall]]
- [[NZBHydra v1|Extras: NZBHydra]]
- [[Plex Requests|Extras: Plex Requests]]
- [[Sickbeard MP4 Automator|Extra: Sickbeard MP4 Automator]]
- [[SABnzbd|Extras: SABnzbd]]
- [[Traktarr|Extras: Traktarr]]

## Misc ##
- [[Nativefier]]

## Community-Submitted ##
See [[Community Wiki|https://github.com/Cloudbox/Community/wiki]].

## Reference ##
- [[Cloudbox Paths|Reference: Cloudbox Paths]]
- [[Cloudbox Ansible Tags|Reference: Cloudbox Ansible Tags]]
- [[Cloudbox Tools|Reference: Cloudbox Tools]] (work in progress)
- [[Cloudbox Ports|Reference: Cloudbox Ports]]
- [[Cloudbox Config Files|Reference: Cloudbox Config Files]]
- [[Cloudbox Settings|Reference: Cloudbox Settings]]

## Troubleshooting ##
- [[FAQ]]
- [[FAQ - Archived]]
- [[502 errors]]
- [[Logs]]
- [[Low Disk Space]]

## Links ##
- [Website](https://cloudbox.works)
- [Community Repo](https://github.com/Cloudbox/Community)
- [Discord](https://discord.io/cloudbox)
- [Reddit](https://reddit.com/r/Cloudbox)