In case you wanted to revoke the SSL certificates/keys for some reason (e.g. using a domain that has been already used for one Cloudbox server on another server), this guide will show you how.

Note: This is not required if you are simply [[Migrating Cloudbox]] to another server, via [[Backup/Restore|Cloudbox Backup and Restore]], and keeping the same domain name. 



Revoking keys for the domain:

1. Run the following script:

   ```bash
   /opt/scripts/nginx-proxy/revoke_certs.sh
   ```

   _Note: Do not run this as root (i.e. sudo)._

2. If asked, chose `y` to delete the certificates.

   ```
   -------------------------------------------------------------------------------
   Would you like to delete the cert(s) you just revoked?
   -------------------------------------------------------------------------------
   (Y)es (recommended)/(N)o: Y
   ```
