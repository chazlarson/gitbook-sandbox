Before Cloudbox can be installed, the server needs to be on a kernel version of 4.10+ (you can run `uname -r` to check).

If you are running Ubuntu Server 16.04 LTS with HWS Kernel or Ubuntu Server 18.04 LTS, you can skip this page.

_Note: You'll need to update the kernel a different way if you are using: [[Scaleway|FAQ#if-you-are-using-a-scaleway-server]] or [[OVH|FAQ#if-you-are-using-an-ovh-server]]._



---

## Update Kernel via Cloudbox

1. Run the following command:

    ```bash
    cd ~/cloudbox
    ```

1. Run the following command:

    ```bash
    sudo ansible-playbook cloudbox.yml --tags kernel
    ```
   _Note: This may take a while to complete._

1. Once the kernel update is done, the server will reboot automatically. If it doesn't, run the following command:

    ```bash
    sudo reboot
     ```

---

## Update Kernel Manually


1. Run the following command:

    ```bash
    sudo apt-get upgrade linux-generic-hwe-16.04
    ```

   _Note: This may take a while to complete._

1. Once the kernel update is done, the server will need to be rebooted:

    ```bash
    sudo reboot
     ```
