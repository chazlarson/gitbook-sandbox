This will install the rest of Cloudbox. 

**NOTE: You should NOT be logged into your server as `root` at this point.  You should be logged in as the user you created/specified in the [[preinstall|Install: Preinstall]].**


1. To start the install, run the following command:

   ```bash
   cb install cloudbox
   ```
   **NOTE**: _Pay attention to the output_, it may require you to run it more than once in some cases, for example if settings have changed. 

1. <details><summary>If you did not enter your Plex credentials in [[accounts.yml|Install: accounts.yml]] ...</summary>


   1. When asked for a Plex Claim Token (_not the same as a Plex login token - a Plex Claim Token starts with `CLAIM_`_), go to https://plex.tv/claim, login to your Plex account if required, copy the claim token, and paste it at the prompt. 

      _Note 1: You may not see the claim token after pasting it. If that occurs, assume it pasted OK and press enter to continue._

      _Note 2: If you make a mistake here, see [[here|FAQ#if-you-are-unable-to-find-your-plex-server]]._

      ![Plex Claim Token Prompt 1](https://i.imgur.com/2r3ShsU.png)

      ![Plex Claim Token](https://i.imgur.com/UgwP2Ip.png)

      ![Plex Claim Token Prompt 2](https://i.imgur.com/iJnsiYT.png)

   1. The next task on the screen will show you what claim token was submitted (in lowercase) and it will continue with the rest of the Cloudbox install.

      ![Plex Claim Token Shown](https://i.imgur.com/VNXiCDZ.png)

   _Note: After install, if you do not see your Plex server after logging in, then Plex claim token was likely entered-in incorrectly. To fix this, see [[here|FAQ#if-you-are-unable-to-find-your-plex-server]]._

   </details> 

1. Reboot after install completes (this is especially important for new installs):

    ```bash
    sudo reboot
     ```

1. After the reboot, the containers should start up and all apps should be available at their subdomains.  **THIS CAN TAKE SOME TIME**, particularly on first install, since certificates need to be retrieved for all the subdomains.  Give it a few minutes.  If, after 10 minutes, you still can't connect to the applications, log in and verify that the containers are running:

    ```bash
    docker ps
    ```

    That should show you a list of all the containers with status.  If the list is empty, run the install command above again.  Chances are it terminated early with a message of some sort.

