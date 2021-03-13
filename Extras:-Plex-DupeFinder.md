<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:1 -->

1. [Introduction](#1-introduction)
2. [Install](#2-install)
3. [Config](#3-config)
	- [Location](#location)
	- [Example](#example)
	- [Details](#details)
	   - [Audio Codec Scores](#audio-codec-scores)
	   - [Auto Delete](#auto-delete)
	   - [Filename Scores](#filename-scores)
	   - [Plex Sections](#plex-sections)
	   - [Plex Server URL](#plex-server-url)
	   - [Plex Token](#plex-token)
	   - [Filesize Scores](#filesize-scores)
	   - [Skip List](#skip-list)
	   - [Video Codec Scores](#video-codec-scores)
	   - [Video Resolution Scoring](#video-resolution-scoring)
4. [Plex](#4-plex)
5. [Run Plex DupeFinder](#5-run-plex-dupefinder)

<!-- /TOC -->


# 1. Introduction

[Plex DupeFinder](https://github.com/l3uddz/plex_dupefinder/) (by [l3uddz](https://github.com/l3uddz/)) is a python app that finds duplicate versions of media (TV episodes and movies) in your Plex Library and tells Plex to remove the lowest quality versions (based on a scoring algorithm), either automatically or interactively (i.e. with a prompt on each find), leaving you with one high quality media file.

[![](https://i.imgur.com/d1sDNlE.png)](https://i.imgur.com/d1sDNlE.png)


_Note: For Mediabox/Feederbox setups, this can be install in either system._


The scoring is based on: non-configurable and configurable parameters.

  - Non-configurable parameters are: _bitrate_, _duration_, _height_, _width_, and _audio channel_.

  - Configurable parameters are: _audio codec scores_, _video codec scores_, _video resolution scores_, _filename scores_, and _file sizes_ (can only be toggled on or off).

  - Note: bitrate, duration, height, width, audio channel, audio and video codecs, video resolutions (e.g. SD, 480p, 720p, 1080p, 4K, etc), and file sizes are all taken from the metadata Plex retrieves during media analysis.

---
Demo:

[![asciicast](https://asciinema.org/a/180157.png)](https://asciinema.org/a/180157?cols=180&rows=50)


# 2. Install

Run the following commands:

  ```bash
  cd ~/cloudbox/
  sudo ansible-playbook cloudbox.yml --tags plex_dupefinder
  ```

# 3. Config


## Location

   ```bash
   /opt/plex_dupefinder/config.json
   ```


## Example

```json
{
    "AUDIO_CODEC_SCORES": {
        "aac": 1000,
        "ac3": 1000,
        "dca": 2000,
        "dca-ma": 4000,
        "eac3": 1250,
        "flac": 2500,
        "mp2": 500,
        "mp3": 1000,
        "pcm": 2500,
        "truehd": 4500,
        "Unknown": 0,
        "wmapro": 200
    },
    "AUTO_DELETE": false,
    "FIND_DUPLICATE_FILEPATHS_ONLY": false,
    "FILENAME_SCORES": {
        "*.avi": -1000,
        "*.ts": -1000,
        "*.vob": -5000,
        "*1080p*BluRay*": 15000,
        "*720p*BluRay*": 10000,
        "*dvd*": -1000,
        "*HDTV*": -1000,
        "*PROPER*": 1500,
        "*Remux*": 20000,
        "*REPACK*": 1500,
        "*WEB*CasStudio*": 5000,
        "*WEB*KINGS*": 5000,
        "*WEB*NTB*": 5000,
        "*WEB*QOQ*": 5000,
        "*WEB*SiGMA*": 5000,
        "*WEB*TBS*": -1000,
        "*WEB*TROLLHD*": 2500,
        "*WEB*VISUM*": 5000
    },
    "PLEX_LIBRARIES": [
        "Movies",
        "TV"
    ],
    "PLEX_SERVER": "https://plex.yourdomain.com",
    "PLEX_TOKEN": "",
    "SCORE_FILESIZE": true,
    "SKIP_LIST": [],
    "VIDEO_CODEC_SCORES": {
        "h264": 10000,
        "h265": 5000,
        "hevc": 5000,
        "mpeg1video": 250,
        "mpeg2video": 250,
        "mpeg4": 500,
        "msmpeg4": 100,
        "msmpeg4v2": 100,
        "msmpeg4v3": 100,
        "Unknown": 0,
        "vc1": 3000,
        "vp9": 1000,
        "wmv2": 250,
        "wmv3": 250
    },
    "VIDEO_RESOLUTION_SCORES": {
        "480": 3000,
        "720": 5000,
        "1080": 10000,
        "4k": 20000,
        "sd": 1000,
        "Unknown": 0
    }
}
```

## Details

### Audio Codec Scores

- You can set `AUDIO_CODEC_SCORES` to your preference.

- The default settings should be sufficient for most.


### Auto Delete

- Under `AUTO_DELETE`, set your desired option.

  - `"AUTO_DELETE": true,`  - Plex DupeFinder will run in automatic mode.

  - `"AUTO_DELETE": false,` -  Plex DupeFinder will run in interactive mode. (Default)

    - Options:

      - Skip (i.e. keep both): `0`

      - Choose the best one (and delete the rest): `b`

      - Select the item to keep (and delete the rest): `#` (i.e. `1`, `2`, `3`, etc).

### Find Duplicate File Paths Only

- Finds duplicates that only share the same file path.

  ```json
  "FIND_DUPLICATE_FILEPATHS_ONLY": false,
  ```

- This option has a very limited use case, i.e. in instances where Plex may have glitched and created multiple duplicates of the same media item.

- If using this setting, we recommend using UnionFS-Fuse that can generate whiteout files (`*_HIDDEN~`) to prevent the deletion of the actual file on the system. The `_HIDDEN~` files can then be removed afterwards or even during the dupe cleanup (e.g. `watch -n 5 rm -rf /mnt/local/.unionfs-fuse/*`).

- The default settings should be sufficient for most.

### Filename Scores

- You can set `FILENAME_SCORES` to your preference. 

- The default settings should be sufficient for most.


### Plex Libraries

1. Go to Plex and get all the names of your Plex Libraries you want to find duplicates in.

   - Example Library:

     ![](https://i.imgur.com/JFRTD1m.png)

1. Under `PLEX_LIBRARIES`, add in a list of Plex libraries that you want scanned for duplicates.

   - Format:

     ```
     "PLEX_LIBRARIES": [
       "LIBRARY_NAME_1",
       "LIBRARY_NAME_2"
     ],
     ```

   - Example:

     ```json
     "PLEX_LIBRARIES": [
       "Movies",
       "TV"
     ],
     ```

### Plex Server URL

- Pre-filled with your Plex server's URL.

### Plex Token

1. Obtain a Plex Access Token: See [[Plex Access Token]].

2. Add the Plex Access Token to `"PLEX_TOKEN"` so that it now appears as `"PLEX_TOKEN": "xxxxxxxxxxxxxx",`.

      - Note: Make sure it is within the quotes (`"`) and there is a comma (`,`) after it.

### Filesize Scores

- `"SCORE_FILESIZE": true` will add more points to the overall score based on the actual file size.

-  Note: In some situations (e.g. a bad encode resulting in a large size), this may be something you want to turn it off (`false`). However, the default settings (i.e. `true`) should be sufficient for most.

- The default settings should be sufficient for most.

### Skip List

- In Auto Delete mode, any file paths matching the patterns (i.e folders), listed in `SKIP_LIST`, will be ignored.

- Example:

  ```json
  "SKIP_LIST": ["/Movies4K/"]
  ```

- The default settings should be sufficient for most.


### Video Codec Scores

- You can set `VIDEO_CODEC_SCORES` to your preference. 

- The default settings should be sufficient for most.

### Video Resolution Scoring

- You can set `VIDEO_RESOLUTION_SCORES` to your preference. 

- The default settings should be sufficient for most.

# 4. Plex 

You will need to make sure that "Allow media deletion" is enabled in Plex.

1. In Plex, click the Settings icon (top right) -> "Server" (top) -> "Library" (left).

1. Set the following:

   - "Allow media deletion": `enabled`

1. Click "SAVE CHANGES".

    ![](http://i.imgur.com/D82n8vh.png)


# 5. Run Plex DupeFinder

- Simply run the following command:

  ```
  plex_dupefinder
  ```