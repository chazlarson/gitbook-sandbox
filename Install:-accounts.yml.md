
##  Overview of accounts.yml ##


```yaml
---
user:
  name: seed
  pass: password123
  domain: testcloudbox.ml
  email: your@email.com
cloudflare:
  email:
  api:
plex:
  user:
  pass:
pushover:
  app_token:
  user_key:
  priority:
apprise:
```
## Editing accounts.yml ##

#### NOTE: The user defined in this file should NOT be `root`. ####
#### NOTE: You will need to edit everything shown above to reflect your domain, email, user, and password. ####
#### IMPORTANT: Enter a password for the user.  Don't leave it blank. Even if you are planning to use SSH keys to connect to your box.  This user and password are used to set up authentication for some applications in this repo and Community, and a blank password may cause trouble there. ####
#### IMPORTANT: This is a YAML file, and values you can enter here are subject to YAML file format rules.  If you use special characters in your password, wrap the password in quotes [or escape the characters correctly, if you are familiar with that concept].  It would be easiest to avoid using quote characters within your password. ####

<details>
  <summary>Examples:</summary>
    <br />

```
  pass: MyP4s5w0rd1s4w350m3
  pass: "!@#$%^&*"
  pass: multiple words work fine unquoted
  pass: "or quote them to be safe"
```
There are a variety of characters that YAML does not allow as the first character of an unquoted string.  Any of the following will result in errors:
```
  pass: 'WhateverWhatever 
  pass: "WhateverWhatever
  pass: [WhateverWhatever
  pass: ]WhateverWhatever
  pass: {WhateverWhatever
  pass: }WhateverWhatever
  pass: >WhateverWhatever
  pass: |WhateverWhatever
  pass: *WhateverWhatever
  pass: &WhateverWhatever
  pass: !WhateverWhatever
  pass: %WhateverWhatever
  pass: `WhateverWhatever
  pass: @WhateverWhatever
  pass: ,WhateverWhatever
  pass: #WhateverWhatever
```
For the most part, these will report a sensible error pointing to the specific problem.  Wrapping the password in quotes would eliminate that error for all but the first two:
```
  pass: ",WhateverWhatever"
   etc.
```

The last case will fail in a non-obvious way; the userdata validation will complain that you haven't entered a password because Ansible doesn't read what looks like a comment.  As far as Ansible is concerned, these are all equivalent:

```
  pass: 
  pass: #Whatever #this is my super secret password
  pass: #Whatever
```

These would work fine:
```
  pass: "#Whatever" #this is my super secret password
  pass: "#Whatever"
```

If you really want to use quote characters in your password, refer to a YAML syntax reference.  There are plenty of options for secure passwords without including those two characters, and given the requirement to escape them properly we recommend you just avoid them.

[[Relevant XKCD|https://xkcd.com/936/]]

</details>

#### NOTE: Formatting [notably spacing] is significant in this file.  There needs to be a space between `key:` and `value` as shown above. Leaving the space out will result in parsing errors that may present in unclear ways, even though the file may pass YAML validation. Missing spaces in YAML config files is a routine source of support issues. ####



1. Go to the Cloudbox folder:

   ```bash
   cd ~/cloudbox/
   ```

1. Open the file for editing:

   - For plain text `accounts.yml`:

     ```bash
     nano accounts.yml
     ```

   - For encrypted `accounts.yml` [encryption of this file is covered later; if this is your first install, it will not be set up yet and you should use the "plain text" option]:

     ```bash
     ansible-vault edit accounts.yml
     ```

1. When done editing, save the file: <kbd class="platform-all">Ctrl + X</kbd> <kbd class="platform-all">Y</kbd> <kbd class="platform-all">Enter</kbd>.


##  Options in accounts.yml

- `user`: User information.

   - `name`: User name for the server. 

      - If user account with this name does not already exist, it will be created during install. 

      - Also used to create first-time logins for NZBGet, ruTorrent, NZBHydra2, and potentially other apps.

      - Default is `seed`. 

      - This parameter is **required**.

   - `pass`: Password for the user account and for misc apps.

       - Sets password for the server's user account when creating a new account. This will not change the password of an existing one. 

      - Also used to create first-time logins for NZBGet, ruTorrent, NZBHydra2, and potentially other apps.

      - This parameter is **required**.

   - `domain`: Domain name for the Cloudbox server. 

      - If you don't have one, see [[here|Prerequisites: Domain Name]].

      - This should be the domain "below" the cloudbox subdomains.  For example, if you want to access Sonarr at "sonarr.domain.tld", enter "domain.tld".  If you want "sonarr.foo.domain.tld", enter "foo.domain.tld".

      - This parameter is **required**.

   - `email`: E-mail address. 

      - This is used for the Let's Encrypt SSL certificates.

      - It does not have to be an email address at the domain above.

      - This parameter is **required**.

- `cloudflare`: Cloudflare Account

   - Fill this in to have Cloudbox add subdomains on Cloudflare, automatically; leave it blank, to have all Cloudflare related functions disabled. 

   - Note: CDN (i.e. proxy) will not be turned on, by default, but you may turn them on later (see [[here|Prerequisites: Cloudflare#post-setup]]).

   - `email`: E-mail address used for the Cloudflare account. 

   - `api`: [[API Token|Prerequisites: Cloudflare]]. 

   - This parameter is optional. 

   - Default is blank.

- `plex`: Plex.tv account credentials. 

   - This will be used to 1) claim the Plex server under your username, and 2) generate Plex Access Tokens for apps such as Plex Autoscan, etc. 

  - `user` - Plex username or email address on the profile.

  - `pass` - Plex password.

  - This parameter is optional. 

  - #### The new Two-Factor Authentication [TFA] system added by Plex will prevent these automated operations from succeeding.  The Plex article [[introducing TFA|https://support.plex.tv/articles/two-factor-authentication/]] has a possible workaround.  If successful, you will need to perform that workaround every time you run the `plex` tag.  You can also disable TFA while you run the cloudbox setup [or the plex tag] and then re-enable it when complete.

- `pushover`: Pushover settings. 

  - This will be used to send out messages during certain tasks (e.g. backup). 

  - `app_token` - Pushover Application API Token (create a new application for Cloudbox). 

  - `user_key` - Pushover User Key. 

  - `priority` - Priority level for messages. 

    - Choices are: `-2`, `-1`, `0`, `1`, and `2`. 

    - Default is blank (i.e. `0`).

  - This parameter is optional. 

- `apprise`: apprise url. 

  - This will be used to send out messages during certain tasks (e.g. backup). 

  - This parameter is not nested like the others in this file. 

  - This parameter is optional. 

