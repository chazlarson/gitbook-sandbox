The following guide allows setting up basic HTTP authentication for any subdomain. You can use this to secure Docker web apps that don't have native login support.

To setup HTTP auth for a subdomain: 

- Run the following command:

  ```
  htpasswd -c /opt/nginx-proxy/htpasswd/SUBDOMAIN.DOMAIN.COM USERNAME
  ```

  Replacing _SUBDOMAIN.DOMAIN.COM_ with the subdomain and domain that you wish to secure with the given _USERNAME_. 

- You will then be prompted for a password and asked to confirm.

- This will create the following encrypted password file: `/opt/nginx-proxy/htpasswd/subdomain.yourdomain.com`.

- Restart the relevant Docker container for the login to take effect

  ```
  docker restart APPNAME
  ```

- To remove HTTP authentication for a subdomain, simply remove the file from `/opt/nginx-proxy/htpasswd/` and restart the relevant Docker container.
