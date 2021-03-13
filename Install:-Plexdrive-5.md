[Plexdrive](https://github.com/dweidenfeld/plexdrive) (by Dominik Weidenfeld) is an app that mounts Google Drive on a server. It works better than others mounting solutions because it caches the stream data for smooth playback of media and and prevention Google Drive API bans.


1. Create a [[Google Drive API Client ID and Client Secret]] for Plexdrive.

    _Note 1: this will be different from the Rclone one. You can use the same Google account; but just create a different project for Plexdrive._


    _Note 2: It is recommended that you create another set of Client ID/Secret separate from the one you used for Rclone._ 

1. Run the following command:

    ```bash
    /opt/plexdrive5/plexdrive mount -v 3 --refresh-interval=1m --chunk-check-threads=8 --chunk-load-threads=8 --chunk-load-ahead=4 --max-chunks=100 --fuse-options=allow_other,read_only --config=/opt/plexdrive5 --cache-file=/opt/plexdrive5/cache.bolt /mnt/remote
    ```

   [![](https://i.imgur.com/NdPwVpF.png)](https://i.imgur.com/NdPwVpF.png)


1. At `Enter your generated client ID:`, paste in the Google API Client ID from Step #1 and press <kbd class="platform-all">Enter</kbd>.

1. At `Enter your generated client secret:`, paste in the Google API Client Secret from Step #1 and press <kbd class="platform-all">Enter</kbd>.


   [![](https://i.imgur.com/NGqtXbq.png)](https://i.imgur.com/NGqtXbq.png)

1. Copy the link on the screen  and paste it in your host computer's internet browser. Login with your Google account, if asked, and click `Allow`. You will copy the `authorization code` from your browser, paste it at the prompt, and press <kbd class="platform-all">Enter</kbd>.


   [![](https://i.imgur.com/CJzgkhn.png)](https://i.imgur.com/CJzgkhn.png)


   [![](https://i.imgur.com/eN9pfqo.png)](https://i.imgur.com/eN9pfqo.png)

   Note 1: You must use the same Google account as the one you are planning to use for Google Drive (see [[Prerequisites|Prerequisites: Cloud Storage]]).

   Note 2: If you keep getting the prompt for the authorization code or any other type of error, you might have used an incorrect Client ID/Secret. Remove the `config.json` and `token.json` files from `/opt/plexdrive5/` and retry Step #2.


1. When you see `First cache build process started...`, press `ctrl`+`c` on your keyboard to exit.

   [![](http://i.imgur.com/bDTmXbT.png)](http://i.imgur.com/bDTmXbT.png)

    Note: Any errors, such as, `WARNING: Could not get object root from API` or `mount helper error`, means this failed somewhere and you need to figure out why.

1. Enable the Plexdrive service:

    ```bash
    sudo systemctl enable plexdrive5
    ```

1. Start the Plexdrive service:

    ```bash
    sudo systemctl start plexdrive5
    ```

1. Verify Plexdrive is running ok:

    ```bash
    sudo systemctl status plexdrive5
    ```

    You should see it as being `Active: active (running)`.


   [![](https://i.imgur.com/1p0oUno.png)](https://i.imgur.com/1p0oUno.png)

    ```bash
   plexdrive5.service - Plexdrive 5
   Loaded: loaded (/etc/systemd/system/plexdrive5.service; enabled; vendor preset: enabled)
   Active: active (running) since Sat 2017-10-14 12:41:01 CEST; 8h ago
   Main PID: 1025 (plexdrive)
   Tasks: 21
   Memory: 2.7G
   CPU: 23.494s
   CGroup: /system.slice/plexdrive5.service
           └─1025 /opt/plexdrive5/plexdrive mount -v 3 --refresh-interval=1m --chunk-check-threads=8 --chunk-load-threads=8 --chunk-
    ```

    _Note: If you see an error here, check the [[FAQ|FAQ#plexdrive]] for possible solutions._

1. Restart Unionfs:

    ```bash
    sudo systemctl restart unionfs
    ```

1. Restart Docker containers:

    ```bash
    docker restart $(docker ps --format '{{ .Names}}' --filter label=com.github.cloudbox.cloudbox_managed=true | xargs echo -n)
    ```

1. After the cache is built (see [[log|Logs#plexdrive]]), all your media files (on the server and on Google Drive - combined) will start showing up under `/mnt/unionfs/Media/`.

   _Note: If your media files are not showing up, then either something went wrong during the setup of Plexdrive (i.e. this page) or your media is not located in the correct folder in Google Drive (see [[Prerequisites|Prerequisites: Cloud Storage]] and [[Paths|Basics: Cloudbox Paths#google-drive-paths]])._
