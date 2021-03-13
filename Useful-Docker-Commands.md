# Docker Commands

#### Stop all docker containers

```
docker stop $(docker ps -a -q)
```

#### Start all docker containers

```
docker start $(docker ps -a -q)
```

#### Start all but one container (e.g. All docker containers except Watchtower)

```
docker start  $(comm -13 <(docker ps -a -q --filter="name=watchtower" | sort) <(docker ps -a -q | sort))
```

#### Remove all docker containers - once they are stopped (be careful)

```
docker rm $(docker ps -a -q)
```

#### Forcefully, Remove all docker containers  (be careful)

```
docker rm -f $(docker ps -a -q)
```

#### Restart only the running containers

```
/opt/scripts/docker/restart_containers.sh
```

# Docker Logs

Find the container name: `docker ps -a`


Live log (from the beginning of the log):
```
docker logs -follow <container_name>
```

Live log (from the last 10 lines of the log):
```
docker logs --follow --tail 100 <container_name>
```

Live log (from the last 10 lines of the log) - abbreviated:
```
docker logs -f --tail 100 <container_name>
```

# Removing Docker Containers

Don't want a certain docker container? You can remove it with the follow steps.

_Note: Certain docker containers are essential to Cloudbox  (e.g. nginx-proxy, letsencrypt)._

Via Command line:
- Get a list of docker container's installed: `docker ps -a`
- Remove the one you don't want (where `<name>` is replaced with the docker container's name): `docker stop <name> && docker rm <name>`

Via Portainer:
- https://portainer._yourdomain.com_
- "Containers" --> make your selection --> "Remove"








# Misc

## Let's Encrypt

To display information on existing certificates:

```
docker exec letsencrypt /app/cert_status
```

To force renew certificates that need to be renewed:

```
docker exec letsencrypt /app/signal_le_service
```

To force renew all certifications:

```
docker exec letsencrypt /app/force_renew
```






## Watchtower

Tool to automaticaly update Docker images and containers.

Note: We recommend you manually update the docker images and containers via their [[Ansible tags|Updating Cloudbox Apps]]. Updating Docker containers with Watchtower has been known to cause data corruption. So use at your own risk.

```
docker start watchtower && docker logs -f watchtower
```

Wait 15 secs for it to finish updating all images except rutorrent (it ignores).. then:

```
docker stop watchtower
```

If no updates, stop anyway.
