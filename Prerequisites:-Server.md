# Getting a Server

Some points below:


- You will need a dedicated server, from a server provider (e.g. Hetzner, kimsufi, OVH, etc), installed with Ubuntu Server [16.04](http://releases.ubuntu.com/16.04/) or [18.04](http://releases.ubuntu.com/18.04/). Some non-Ubuntu Debian systems will also work. 

  - Note: Ubuntu 18.10 is currently having issues with Docker python module install. This should be avoided for now. For more info, see [here](https://github.com/ansible/ansible/issues/37640).

  - Note: Ubuntu 20.04 is NOT SUPPORTED. [NOTE: Still true here in March of 2021.  Addressing this is relatively low priority.]

- Best results are seen with an actual dedicated server, not a VPS like those available from Linode, Vultr, or the like.  Linodes, Vultr "Cloud Compute", Hetzner "Cloud Servers", and probably others like them, in particular, are known to _not_ work in at least one significant way; nzbget reports 0 available disk space while Sonarr, Radarr, and tools like `df` and `du` report disk space as expected.

- Server should be a completely fresh OS install. Do not try to install any dependencies on your own, Cloudbox will do that for you. 

- Cloudbox only supports x64 (i.e. Intel or AMD 64) machines. ARM based hardware [such as the Raspberry Pi] is not supported.

- Get a server with at least 100GB+ of hard disk space. Even though media is uploaded to the cloud, there is still a need local storage for things like app data and backups. 

  Practically, you should have more like 500GB of space available _at a minimum_.

  Cloudplow's default folder size threshold, to upload media to the cloud, is set at 200GB. To lower that, you'll need to go [[here|Cloudplow#modify-upload-threshold-and-interval]]

  If you are planning to use Usenet, SSD should be considered required, and NVME highly recommended.  Usenet is extremely disk I/O intensive.

  If you are planning to use torrents, you should have much more disk space than that available for seeding.  Your seeding torrents will not be moved to your cloud storage; they will consume local disk space as long as they are seeding. 

  If you are installing as a Feederbox/Mediabox setup rather than the all-in-one Cloudbox, the disk requirements change a bit. Downloading drives disk requirements on the Feederbox [as discussed above] and primarily the Plex/Emby metadata drives the disk requirements on the Mediabox.  Depending on the size of your library, that metadata can be quite large.

-  If you are setting this up on a home server, verify, **before installing Cloudbox**:
   1. Make sure your ISP doesn't block ports 80 and 443 [if your ISP blocks these ports, it won't work.]
   1. Make sure that your router supports hairpin NAT [if this isn't supported, you won't be able to access apps via subdomain from inside your network]
   1. Open the relevant [[ports|Reference: Cloudbox Ports]] (eg `80`, `443`, etc) in your [router](https://portforward.com/router.htm)/firewall and forward them to the IP of the box on which you want to install Cloudbox, **before installing Cloudbox**.
   1. Point your domain at your home IP and configure some dynamic DNS software to keep it updated.  Cloudbox has a dynamic dns client available [it's not installed by default], but there are many ways to set this up.  Make sure that DNS has propagated and your domain returns your home IP via `ping` or something like it, **before installing Cloudbox**.

- If you are using a Scaleway server, read [[this|FAQ#if-you-are-using-a-scaleway-server]].





# Tips

## Ubuntu

### 16.04

- If given an option like below, choose the one with the `HWE Kernel`. 

     ![](https://i.imgur.com/nBCsD9E.png)

- If you get an option like below, select choose `ubuntu-1604-xenial-64-minimal`.

  ![](https://i.imgur.com/DcZAAWM.png)

- Install OpenSSH server if asked. 

### 18.04

- If you get an option like below, select choose `ubuntu-1804-bionic-64-minimal`.

  ![](https://i.imgur.com/DcZAAWM.png)

- Install OpenSSH server if asked. 

## Partitioning:
- If you have multiple hard drives on the server (eg. 2 x 4 TB), put them in RAID 0 to maximize space and speed (you don't need redundancy as you can schedule backups of Cloudbox).

- Set all available space to `/` (remove `/home` and `/data` partitions).

- Leave ample space in `/boot` (e.g. 2+ GB).

- putting the `/opt` directory on a `btrfs` partition can dramatically reduce the amount of time your containers are down during backup.

- Examples

   - Online.net

     ![](https://i.imgur.com/1rDCs4z.png)

   - OVH

     ![](https://i.imgur.com/GRTjQvt.png)

     ![](https://i.imgur.com/UqR2GCv.png)

   - Hetzner installimage
     ```#
     # Hetzner Online GmbH - installimage
     #
     # This file contains the configuration used to install this
     # system via installimage script. Comments have been removed.
     #
     # More information about the installimage script and
     # automatic installations can be found in our wiki:
     #
     # http://wiki.hetzner.de/index.php/Installimage
     #
     
     DRIVE1 /dev/nvme0n1
     DRIVE2 /dev/nvme1n1
     SWRAID 1
     SWRAIDLEVEL 0
     HOSTNAME cb.domain.com
     PART /boot  ext4     512M
     PART lvm    vg0       all
     LV vg0   swap   swap      swap         8G
     LV vg0   root    /     ext4      all
     IMAGE /root/.oldroot/nfs/install/../images/Ubuntu-1804-bionic-64-minimal.tar.gz
     ```

   - Hetzner installimage (with a separate 250G partition for `/opt` utilizing BTRFS for snapshot backups)

     ```#
     # Hetzner Online GmbH - installimage
     #
     # This file contains the configuration used to install this
     # system via installimage script. Comments have been removed.
     #
     # More information about the installimage script and
     # automatic installations can be found in our wiki:
     #
     # http://wiki.hetzner.de/index.php/Installimage
     #
     
     DRIVE1 /dev/nvme0n1
     DRIVE2 /dev/nvme1n1
     SWRAID 1
     SWRAIDLEVEL 0
     HOSTNAME cb.domain.com
     PART /boot  ext4     512M
     PART lvm    vg0       all
     LV vg0   swap   swap      swap         8G
     LV vg0   opt   /opt     btrfs         250G
     LV vg0   root    /     ext4      all
     IMAGE /root/.oldroot/nfs/install/../images/Ubuntu-1804-bionic-64-minimal.tar.gz
     ```