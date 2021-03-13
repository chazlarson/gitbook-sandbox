## General Info

It is recommended to assign all your disk space to `/`, as all of your imported media and app data will be saved to `/mnt/local/` and `/opt/`,  respectively.


Note 1: **ALL** folders/paths mentioned below, and elsewhere on the wiki, are **CASE SENSITIVE** (e.g. Google Drive: `Media` not `media`, `Movies` not `movies`, `TV` not `tv`; Plex Requests: `/logs` not `/Logs`, etc). This is important, or else apps like Plex, Sonarr, and Radarr will not be able find your media.

Note 2: This wiki uses `~/` interchangeably with `/home/<username>/`, which is defined as `/home/{{user}}/` in Ansible syntax (as used in [[settings.yml|Install: Settings]]). So if your user name was `seed`, your `~/` path would be `/home/seed/`.

## Google Drive Paths




```
Media
├── Movies
├── Music
└── TV
```

![](https://i.imgur.com/kwnNjni.png)


| Path  <pre>                 </pre>                 | Description  <pre>                                                                                              </pre>                                                                                                                                                          |
|:---------------------- |:------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `/Media/`     | Location of all your media folders.                                                                                                                         |
| `/Media/Movies/` | Location of all your movies (folder format: `/Media/Movies/Movie Name (year)/movie file.ext`).                                                                                                  |
| `/Media/Music/` | Location of all your music.                                 |
| `/Media/TV/`   | Location of all your TV shows (folder format: `/Media/TV/TV Show Name/Season 00/episode file.ext`). |

_Note: If you would like to customize your Plex libraries differently, see [[Customizing Plex Libraries]]._


## Local Paths

```
mnt
├──local
|  └── Media
├──remote
|  └── Media
└──unionfs
   └── Media
```

### Media





| <pre>                 </pre> Path                   | <pre>                                                                                                 </pre> Description                                                                                                                                                            |
|:---------------------- |:------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `/mnt/local/Media/`     | Location of media stored on the server.  <br /><br />This is the local part of `/mnt/unionfs/Media/`.                                                                                                                        |
| `/mnt/remote/Media/` | Location of media stored on Google Drive (mounted by rclone).                                                                                                  |
| `/mnt/unionfs/Media/`   | Combined folder of local media (`/mnt/local/Media/`) and online media (`/mnt/remote/Media/`). <br /><br /> This is the folder that Plex, Sonarr, and Radarr read when scanning for media.|

_Note: Make sure `/mnt/local/` has enough space to store the imported media (before it is able to move it to Google Drive; see [below](#unionfs-cleaner))._

### Cloudplow


| Path<pre>                 </pre>               | Description <pre>                 </pre>                                                                                                                                                                                      |
|:------------------ |:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/mnt/local/Media/` | Location of media stored on the server. <br /><br /> Size of this path is checked periodically (default 30 min). When the folder size reaches its target (default 200GB), media files are moved off/uploaded to the cloud, freeing up local disk space. |

_Note: For more info, see the [[Cloudplow]] page._


## Docker Paths

The Dockerized app (e.g. Plex) will "see" the **Docker Path**, but that path will actually be the **Host Path** on the server. 

By default, NZB and Torrent downloads are stored in `/mnt/local/downloads/nzbs/` and `/mnt/local/downloads/torrents/`, respectively. However, this can be changed to point elsewhere (e.g. a second hard drive) by editing the [[settings.yml|Install: Settings]] file. But regardless of the download location chosen, the **Docker Path** will always be the same.

_Note: It is advised to leave at least 100GB free on `/opt` for the storage of Docker data_.

### Plex

| Docker Path <pre>                 </pre>   | Host Path <pre>                 </pre>                  | Description <pre>                 </pre>                     |
|:-------------- |:--------------------------- |:---------------------------- |
| `/data/Movies/` | `/mnt/unionfs/Media/Movies/` | Plex reads this for Movies.   |
| `/data/TV/`     | `/mnt/unionfs/Media/TV/`    | Plex reads this for TV Shows. |
| `/data/Music/`   | `/mnt/unionfs/Media/Music/`     | Plex reads this for Music. |


### Sonarr


| Docker Path  <pre>                 </pre>          | Host Path <pre>                                     </pre>                        | Description <pre>                                                                                                                                                             </pre>                                                                |
|:---------------------- |:--------------------------------- |:--------------------------------------------------------------------------- |
| `/tv/`              | `/mnt/unionfs/Media/TV/`       | Sonarr will import to `/tv/`, which is actually `/mnt/unionfs/Media/TV/` on host system. |
| `/downloads/nzbs/`    | `/mnt/local/downloads/nzbs/` (default) | NZB downloads folder as set in [[settings.yml\|Install: Settings]]).  <br /> <br /> For example, when using NZBGet, Sonarr will import from `/downloads/nzbs/nzbget/`, which is essentially `/mnt/local/downloads/nzbs/nzbget/` on host system.                          |
| `/downloads/torrents/` | `/mnt/local/downloads/torrents/` (default) | Torrent downloads folder as set in [[settings.yml\|Install: Settings]]).  <br /> <br /> For example, when using ruTorrent, Sonarr will import from `/downloads/torrents/rutorrent/`, which is essentially `/mnt/local/downloads/torrents/rutorrent/` on host system.                     |


### Radarr


| Docker Path  <pre>                 </pre>          | Host Path <pre>                                     </pre>                        | Description <pre>                                                                                                                                                             </pre>                                                                |
|:---------------------- |:--------------------------------- |:--------------------------------------------------------------------------- |
| `/movies/`              | `/mnt/unionfs/Media/Movies/`       | Radarr will import to `/movies/`, which is actually `/mnt/unionfs/Media/Movies/` on host system. |
| `/downloads/nzbs/`    | `/mnt/local/downloads/nzbs/` (default) | NZB downloads folder as set in [[settings.yml\|Install: Settings]]).  <br /> <br /> For example, when using NZBGet, Radarr will import from `/downloads/nzbs/nzbget/`, which is essentially `/mnt/local/downloads/nzbs/nzbget/` on host system.                          |
| `/downloads/torrents/` | `/mnt/local/downloads/torrents/` (default) | Torrent downloads folder as set in [[settings.yml\|Install: Settings]]).  <br /> <br /> For example, when using ruTorrent, Radarr will import from `/downloads/torrents/rutorrent/`, which is essentially `/mnt/local/downloads/torrents/rutorrent/` on host system.                     |

### Lidarr


| Docker Path  <pre>                 </pre>          | Host Path <pre>                                     </pre>                        | Description <pre>                                                                                                                                                             </pre>                                                                |
|:---------------------- |:--------------------------------- |:--------------------------------------------------------------------------- |
| `/music/`              | `/mnt/unionfs/Media/Music/`       | Lidarr will import to `/music/`, which is actually `/mnt/unionfs/Media/Music/` on host system. |
| `/downloads/nzbs/`    | `/mnt/local/downloads/nzbs/` (default) | NZB downloads folder as set in [[settings.yml\|Install: Settings]]).  <br /> <br /> For example, when using NZBGet, Lidarr will import from `/downloads/nzbs/nzbget/`, which is essentially `/mnt/local/downloads/nzbs/nzbget/` on host system.                          |
| `/downloads/torrents/` | `/mnt/local/downloads/torrents/` (default) | Torrent downloads folder as set in [[settings.yml\|Install: Settings]]).  <br /> <br /> For example, when using ruTorrent, Lidarr will import from `/downloads/torrents/rutorrent/`, which is essentially `/mnt/local/downloads/torrents/rutorrent/` on host system.                     |

### PlexPy (Tautulli)


| Docker Path  <pre>                 </pre>          | Host Path <pre>                                                            </pre>                        | Description <pre>                                     </pre>                                                                |
|:----------- |:-------------------------------------------------------------- |:------------------------------------- |
| `/logs/`     | `/opt/plex/Library/Application Support/Plex Media Server/Logs/`| Location of the Plex logs used by PlexPy.  |


---
