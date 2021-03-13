

# Introduction


Sends autodl-irssi feed to Sonarr/Radarr. 


# Setup

## ruTorrent

- Click the 'autodl-irssi' icon. 

  ![](https://i.imgur.com/60VQHs1.png)

- Select 'Filters'.

  ![](https://i.imgur.com/9Ghy8jp.png)

## autodl-irssi Filters:

### TV


- Choose .torrent action: `Run Program`

- Command: 

  ```
  /scripts/torrents/arrpush.py
  ```

- Arguments: 

  ```
  "http://sonarr:8989" "API_KEY" "$(TorrentName)" "$(TorrentUrl)" "$(TorrentSize)" "$(Tracker)"
  ```

  Replace `API_KEY` with your Sonarr API Key.


- Example: 

  ![](https://i.imgur.com/Yg2kgOC.png)


### Movies


- Choose .torrent action: `Run Program`

- Command: 

  ```
  /scripts/torrents/arrpush.py
  ```

- Arguments (All except PTP and NEBULANCE): 

  ```
  "http://radarr:7878" "API_KEY" "$(TorrentName)" "$(TorrentUrl)" "$(TorrentSize)" "$(Tracker)"
  ```

  Replace `API_KEY` with your Radarr API Key.


- Arguments (PTP or NEBULANCE): 

  ```
  "http://radarr:7878" "API_KEY" "$(TorrentName)" "$(TorrentUrl)" "$(TorrentSize)" "$(Tracker)" "$(TorrentPathName)"
  ```

  Replace `API_KEY` with your Radarr API Key.

# Known Issues / Limitations

ARRpush does not have a way to get a releases name and size from PTP and Nebulance IRC announcements without having to download and extract the torrent file itself. This may lead to high .torrent download usage for these trackers. To work around this, use filters to reduce what ARRpush pushes to Sonarr/Radarr.

- Example: 

  ![](https://i.imgur.com/FnGBpRG.png)



<!--

![](https://i.imgur.com/9EBRiYW.png)


for ipt
i was using
match category
TV/* and Movie/*
if i didnt have the / in movie
it was notifying radarr of XXX/Movie
which ofc i didnt want radarr being told about
so Movie/*
matches all ipt movie cats
and push those to radarr for decision




anyone who has experience with autodl
will know what todo if u just tell them
`sonarr "$(TorrentName)" "$(TorrentUrl)" "$(TorrentSize)" "$(Tracker)"`
as args
and /scripts/arrpush.sh

-->