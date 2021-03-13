502 Errors typically indicate that the docker container is having trouble starting, but another common cause is something some browser extension autofilling the port field in the configuration.  This often happens with Radarr, Sonarr, Lidarr, and possibly other *arrs.

If you find one of the *arr apps giving 502 errors, and the container seems to be running, verify that this configuration still contains the correct port.  To correct this you'll need to edit the config file manually, since you won't be able to access the web UI to do it there.

Here are default config files for the apps mentioned above:

### Radarr
```
➜  ~ cat /opt/radarr/app/config.xml
```

```xml
<Config>
  <LogLevel>Info</LogLevel>
  <Port>7878</Port>
  <UrlBase></UrlBase>
  <BindAddress>*</BindAddress>
  <SslPort>9898</SslPort>
  <EnableSsl>False</EnableSsl>
  <ApiKey>REDACTED</ApiKey>
  <AuthenticationMethod>None</AuthenticationMethod>
  <Branch>develop</Branch>
  <LaunchBrowser>True</LaunchBrowser>
  <SslCertHash></SslCertHash>
  <UpdateMechanism>BuiltIn</UpdateMechanism>
  <UpdateAutomatically>False</UpdateAutomatically>
</Config>
```

### Sonarr
```
➜  ~ cat /opt/sonarr/app/config.xml
```
```xml
<Config>
  <LogLevel>Info</LogLevel>
  <Port>8989</Port>
  <UrlBase></UrlBase>
  <BindAddress>*</BindAddress>
  <SslPort>9898</SslPort>
  <EnableSsl>False</EnableSsl>
  <ApiKey>REDACTED</ApiKey>
  <AuthenticationMethod>None</AuthenticationMethod>
  <UpdateMechanism>Docker</UpdateMechanism>
  <Branch>phantom-develop</Branch>
  <LaunchBrowser>True</LaunchBrowser>
  <SslCertHash></SslCertHash>
</Config>
```

### Lidarr
```
➜  ~ cat /opt/lidarr/app/config.xml
```
```xml
<Config>
  <LogLevel>Info</LogLevel>
  <Port>8686</Port>
  <UrlBase></UrlBase>
  <BindAddress>*</BindAddress>
  <SslPort>6868</SslPort>
  <EnableSsl>False</EnableSsl>
  <ApiKey>REDACTED</ApiKey>
  <AuthenticationMethod>None</AuthenticationMethod>
  <Branch>develop</Branch>
  <LaunchBrowser>True</LaunchBrowser>
  <SslCertHash></SslCertHash>
  <UpdateMechanism>BuiltIn</UpdateMechanism>
</Config>
```

Compare your files to these; if the ports are incorrect, stop the container, edit the config file to correct the port, then restart the container.

For example:
```
docker stop sonarr
nano /opt/sonarr/app/config.xml
docker start sonarr
```