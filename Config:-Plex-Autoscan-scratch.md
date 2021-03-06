```
{
  "DOCKER_NAME": "plex",
  "GDRIVE": {
    "CLIENT_ID": "xxx",
    "CLIENT_SECRET": "xxx",
    "ENABLED": true,
    "IGNORE_PATHS": [],
    "POLL_INTERVAL": 60,
    "SCAN_EXTENSIONS": [
      "webm",
      "mkv",
      "flv",
      "vob",
      "ogv",
      "ogg",
      "drc",
      "gif",
      "gifv",
      "mng",
      "avi",
      "mov",
      "qt",
      "wmv",
      "yuv",
      "rm",
      "rmvb",
      "asf",
      "amv",
      "mp4",
      "m4p",
      "m4v",
      "mpg",
      "mp2",
      "mpeg",
      "mpe",
      "mpv",
      "m2v",
      "m4v",
      "svi",
      "3gp",
      "3g2",
      "mxf",
      "roq",
      "nsv",
      "f4v",
      "f4p",
      "f4a",
      "f4b",
      "mp3",
      "flac",
      "ts"
    ],
    "TEAMDRIVE": false
  },
  "PLEX_ANALYZE_DIRECTORY": true,
  "PLEX_ANALYZE_TYPE": "basic",
  "PLEX_DATABASE_PATH": "/opt/plex/Library/Application Support/Plex Media Server/Plug-in Support/Databases/com.plexapp.plugins.library.db",
  "PLEX_EMPTY_TRASH": true,
  "PLEX_EMPTY_TRASH_CONTROL_FILES": [
    "/mnt/unionfs/mounted.bin"
  ],
  "PLEX_EMPTY_TRASH_MAX_FILES": 100,
  "PLEX_EMPTY_TRASH_ZERO_DELETED": false,
  "PLEX_LD_LIBRARY_PATH": "/usr/lib/plexmediaserver",
  "PLEX_LOCAL_URL": "http://localhost:32400",
  "PLEX_SCANNER": "/usr/lib/plexmediaserver/Plex\\ Media\\ Scanner",
  "PLEX_SECTION_PATH_MAPPINGS": {
    "1": [
      "/Movies/Movies/"
    ],
    "2": [
      "/TV/TV/"
    ],
    "3": [
      "/TV/Kids-Anime/"
    ],
    "4": [
      "/Movies/Movies-Kids/"
    ],
    "5": [
      "/TV/Kids-TV/"
    ],
    "6": [
      "/Movies/Movies-4K/"
    ]
  },
  "PLEX_SUPPORT_DIR": "/var/lib/plexmediaserver/Library/Application\\ Support",
  "PLEX_TOKEN": "xxx",
  "PLEX_USER": "plex",
  "PLEX_WAIT_FOR_EXTERNAL_SCANNERS": true,
  "RCLONE_RC_CACHE_EXPIRE": {
    "ENABLED": false,
    "FILE_EXISTS_TO_REMOTE_MAPPINGS": {},
    "MOUNT_FOLDER": "/mnt/rclone",
    "RC_URL": "http://localhost:5572"
  },
  "RUN_COMMAND_AFTER_SCAN": "",
  "RUN_COMMAND_BEFORE_SCAN": "",
  "SERVER_ALLOW_MANUAL_SCAN": true,
  "SERVER_FILE_CHECK_DELAY": 60,
  "SERVER_FILE_EXIST_PATH_MAPPINGS": {
    "/mnt/unionfs/Media": [
      "/data"
    ]
  },
  "SERVER_IGNORE_LIST": [
    "/.grab/",
    ".DS_Store",
    "Thumbs.db"
  ],
  "SERVER_IP": "0.0.0.0",
  "SERVER_MAX_FILE_CHECKS": 10,
  "SERVER_PASS": "xxx",
  "SERVER_PATH_MAPPINGS": {
  "/data/Movies/Movies/": [
    "/mnt/unionfs/Media/Movies/",
    "My Drive/Media/Movies/"
  ],
  "/data/TV/TV/": [
    "/mnt/unionfs/Media/TV/",
    "My Drive/Media/TV/TV/"
  ],
  "/data/TV/Kids-Anime/": [
    "/mnt/unionfs/Media/TV/Kids-Anime/",
    "My Drive/Media/TV/Kids-Anime/"
  ],
  "/data/Movies/Movies-Kids/": [
    "/mnt/unionfs/Media/Movies/Movies-Kids/",
    "My Drive/Media/Movies/Movies-Kids/"
  ],
  "/data/TV/Kids-TV/": [
    "/mnt/unionfs/Media/TV/Kids-TV/",
    "My Drive/Media/TV/Kids-TV/"
  ],
  "/data/Movies/Movies-4K/": [
    "/mnt/unionfs/Media/Movies/Movies-4K/",
    "My Drive/Media/Movies/Movies-4K/"
  ]
},
  "SERVER_PORT": 3468,
  "SERVER_SCAN_DELAY": 180,
  "SERVER_SCAN_FOLDER_ON_FILE_EXISTS_EXHAUSTION": true,
  "SERVER_SCAN_PRIORITIES": {
  "0": [
    "/TV/TV/"
  ],
  "1": [
    "/TV/Kids-TV/"
  ],
  "2": [
    "/TV/Kids-Anime/"
  ],
  "3": [
    "/Movies/Movies"
  ],
  "4": [
    "/Movies/Movies-Kids/"
  ],
  "5": [
    "Movies/Movies-4K/"
  ]
  },
  "SERVER_USE_SQLITE": true,
  "USE_DOCKER": true,
  "USE_SUDO": false
}
```