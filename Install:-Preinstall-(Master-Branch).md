To run **Preinstall**: 

1. Go into the Cloudbox folder:

   _Note: If you're following the install steps in order, you are already in this directory._

    ```bash
    cd ~/cloudbox
    ```

1. To start the install, run the following command:

   ```bash
   sudo ansible-playbook cloudbox.yml --tags preinstall
   ```

   _Note: The system will reboot at the end if the kernel was updated as part of the preinstall process.  The kernel does not always need to be updated, so the system **may not** reboot._
