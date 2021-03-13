
1. Go into the Cloudbox folder:

    ```bash
    cd ~/cloudbox
    ```

1. To start the install, run the following command:

   ```bash
   sudo ansible-playbook cloudbox.yml --tags feederbox
   ```
1. Reboot after install completes (this is especially important the first time):

    ```bash
    sudo reboot
     ```