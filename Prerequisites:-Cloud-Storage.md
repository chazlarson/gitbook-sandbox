## Provider

Cloudbox can be setup to use any cloud storage provider that [Rclone](https://rclone.org/) supports. However, Google Drive via [G-Suite Business](https://gsuite.google.com/pricing.html) is the popular choice among users.

It is advised that you do NOT use a educational GSuite account or any GSuite account you may buy on the secondary market [eBay and the like].

## Basics

Out of the box, Cloudbox stores the media unencrypted in cloud storage utilizing an Rclone VFS mount to access it. If you prefer your data is stored encrypted, you will need to do some tweaking to the Rclone config.

Media will be stored in `Movies` and `TV` folders, all within a `Media` folder in root (i.e. `/Media`). <a href="#note1" id="note1ref"><sup>[1]</sup></a>  

## Setup

```
Media
├── Movies
├── Music
└── TV
```

- Example from Google Drive:

  ![](https://i.imgur.com/kwnNjni.png)

If you have media in other folders, you can simply move them into these folders via the Cloud Storage Provider's web site.

Note 1: For Google Drive, you can use the [Shift-Z trick](https://www.labnol.org/internet/add-files-multiple-drive-folders/28715/) to "symlink" folders here. 

Note 2: All the paths/folders mentioned here, and elsewhere, are **CASE SENSITIVE** (see  [[Cloudbox Paths|Basics: Cloudbox Paths]]).

---
 <sub> <a id="note1" href="#note1ref"><sup>1</sup></a> If you would like to customize your Plex libraries beyond what is listed above, see [[Customizing Plex Libraries]].</sub>
