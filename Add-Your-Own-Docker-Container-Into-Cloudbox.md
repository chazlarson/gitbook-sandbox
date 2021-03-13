
# Prerequisites:

When you install existing roles in cloudbox, some things get handled behind the scenes for you.  Notably, this includes creating the subdomain[s] at cloudflare and creating the `/opt/APPNAME ` directory tree.

When you add a container manually as outlined on this page, neither of those things will be done for you, so prior to running the docker commands described below you will have to create the `APPNAME.domain.tld` subdomain at cloudflare [or wherever your DNS is] and create the required `/opt/APPNAME ` directory tree.

The examples below are `docker run` commands that you would execute in an SSH session on your server.

If you want to create a role file that you can install like the built-in applications, the [Contribute page in the Community wiki](https://github.com/Cloudbox/Community/wiki/Contribute) outlines the process.

# Format

<pre>
docker run -d  \
	--name=<strong>APPNAME</strong>  \
	--restart=unless-stopped  \
	-e PGID=<strong>1000</strong> -e PUID=<strong>1000</strong>  \
	-v /opt/<strong>APPNAME</strong>:<strong>/CONFIG</strong>  \
	-v /etc/localtime:/etc/localtime:ro  \
        --label com.github.cloudbox.cloudbox_managed=true \
	--network=cloudbox  \
	--network-alias=<strong>APPNAME</strong>  \
	-e VIRTUAL_HOST=<strong>APPNAME.yourdomain.com</strong>  \
	-e VIRTUAL_PORT=<strong>PORT</strong>  \
	-e LETSENCRYPT_HOST=<strong>APPNAME.yourdomain.com</strong>  \
	-e LETSENCRYPT_EMAIL=<strong>your@email.com</strong>  \
	<strong>docker/image</strong>

</pre>

# Format (detailed)

Note: containers will not always use `/config`, nor will they necessarily use everything shown here.  The required volume maps and environment variables will vary by the docker image being used.

<pre>
docker run -d \
    --name <strong>APPNAME</strong> \
    --restart=unless-stopped \
    -e PGID=<strong>1000</strong> -e PUID=<strong>1000</strong> \
    --network=cloudbox \
    --network-alias=<strong>APPNAME</strong> \
    -p <strong>host_port1</strong>:<strong>container_misc_port1</strong> \
    -p <strong>host_port2</strong>:<strong>container_misc_port2</strong> \
    -v /opt/<strong>APPNAME</strong>/:/config \
    -v /mnt/:/mnt/ \
    --label com.github.cloudbox.cloudbox_managed=true \
    -e VIRTUAL_PORT=<strong>container_webadmin_port</strong> \
    -e VIRTUAL_HOST=<strong>APPNAME.yourdomain</strong> \
    -e LETSENCRYPT_HOST=<strong>APPNAME.yourdomain</strong> \
    -e LETSENCRYPT_EMAIL=<strong>your@email.com</strong> \
    <strong>docker-hub-user/repo-name</strong>
</pre>


# Examples


```
docker run -d  \
	--name=thelounge  \
	--restart=unless-stopped  \
	-e PGID=1000 -e PUID=1000  \
	-v /opt/thelounge:/home/lounge/data  \
	-v /etc/localtime:/etc/localtime:ro  \
        --label com.github.cloudbox.cloudbox_managed=true \
	--network=cloudbox  \
	--network-alias=thelounge  \
	-e VIRTUAL_HOST=thelounge.yourdomain.com  \
	-e VIRTUAL_PORT=9000  \
	-e LETSENCRYPT_HOST=thelounge.yourdomain.com  \
	-e LETSENCRYPT_EMAIL=your@email.com  \
	thelounge/lounge:latest
```

```
docker run -d \
	--name=nextcloud  \
	--restart=unless-stopped \
	-v '/opt/nextcloud:/var/www'  \
        --label com.github.cloudbox.cloudbox_managed=true \
	--network=cloudbox  \
	--network-alias=nextcloud  \
	-e 'VIRTUAL_HOST=nextcloud.yourdomain.com'  \
	-e 'VIRTUAL_PORT=80'  \
	-e 'LETSENCRYPT_HOST=nextcloud.yourdomain.com'  \
	-e 'LETSENCRYPT_EMAIL=your@email.com'  \
	nextcloud
```

```
docker run -d  \
        --name=searcharr  \
        --restart=unless-stopped  \
        -v /opt/searcharr/data:/app/data  \
        -v /opt/searcharr/logs:/app/logs  \
        -v /opt/searcharr/settings.py:/app/settings.py  \
        -e TZ=America/New_York  \
        --label com.github.cloudbox.cloudbox_managed=true \
        --network=cloudbox  \
        --network-alias=searcharr  \
        toddrob/searcharr:latest
```

# Details

## Notes

- Replace all `<tags>` with your info.

- All `<container_*>` items are specified by the Docker container.

- Ideally, you want all `<name>` items to have the same name.

- Pick docker images that allow you to specify the PUID/PGID.

- You can break a command into multiple lines with a backslash (`\`) at the end of all the lines except the last one.

## Basics

- `--name=<name>`

- `--restart=unless-stopped`

  - To have it startup automatically, unless the container was previously stopped.

- `-v /etc/localtime:/etc/localtime:ro`

  - To set the docker container's timezone to your host timezone.

- `-e PUID=<your_user_ID> -e PGID=<your_group_ID>`

  - Replace `<user>` and `<group>` to match yours (see [here](FAQ#find-your-user-id-uid-and-group-id-gid)).
- `--label com.github.cloudbox.cloudbox_managed=true`

  - Is used to determine whether the container is shut down or not during Cloudbox backup and other tasks. If you want this container to not be shut down, leave the label out or set it to `false`.

  - If you do decide leave this out or set this to `false`, it will probably be a good idea to store the config files at another location other than `/opt` as a running container could cause issues during Cloudbox Backup. 

## Mount Paths

  Mount paths are in the format of `path/on/host:path/within/container`. You may change the path on host (left side), but not the path set for the container, internally (right side).

  - `-v /opt/<name>:<container_config_path>`

    - This is where your config files will go

    - You will need to:

      - Create the folder: `mkdir /opt/<name>`

      - Set ownership: `sudo chown -R <user>:<group> /opt/<name>`

        - Replace `<user>` and `<group>` to match yours' (see [here](FAQ#find-your-user-id-uid-and-group-id-gid))

      - Set permissions: `sudo chmod -R ugo+X /opt<name>`

  - `-v /mnt/local/downloads/<name>:/downloads/<name>`

    - Only required if your Docker app needs a path for downloads.

    - You will need to set `/downloads/<name>` as the downloads path in your app.

    - This path will be accessible to Sonarr and Radarr.

    - You will need to:

      - Create the folder: `mkdir /mnt/local/downloads/<name>`

      - Set ownership: `sudo chown -R <user>:<group> /mnt/local/downloads/<name>`

        - Replace `<user>` and `<group>` to match yours' (see [here](FAQ#find-your-user-id-uid-and-group-id-gid))

      - Set permissions: `sudo chmod -R ugo+X /mnt/local/downloads/<name>`

## Network

Note: These are important, but leave them out if your docker run command requires `--net=host`.

  - `--network=cloudbox`

  - `--network-alias=<name>`   (aliases are shortcuts to communicate across dockers)

## Ports

  Ports are in the format of `host_port:container_port`.

  - For the main, web admin/page port (e.g. 32400 in Plex):

    - You do not need to specify this port with `-p`. Since this port will not be accessible over the net or from the host. Instead, Nginx-Proxy will redirect the subdomain to it.

    - If you do want the port accessible from the host (but not from the net), simply add `127.0.0.1:` to it and specify it via:

      `-p 127.0.0.1:<host_port>:<container_webadmin_port>`

      If you expose ports to the host like this, make sure they don't conflict with another one on that host.

  - For all other ports:

    - `-p <host_port>:<container_other_ports>`

      - These are accessible from the net.
      
## Nginx Proxy

  - `-e VIRTUAL_PORT=<container_webpage_port>` (the port for the web admin page for the container)

  - `-e VIRTUAL_HOST=<name>.<yourdomain>`

  - `-e LETSENCRYPT_HOST=<name>.<yourdomain>`

  - `-e LETSENCRYPT_EMAIL=<your@email.com>` 

    - This should be a real email address.

You'll need to add the subdomain manually at your DNS provider if you're not using wild-card DNS.
