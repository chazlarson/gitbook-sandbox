**Preinstall** will do the following:

- create a user account (if one does not exist) and add that to the `sudo` group so that it can run privileged commands.

- update the kernel (if necessary). 

- make appropriate GRUB edits (if it's a Hetzner system with Intel iGPU support)

- install [[Rclone|Install: Rclone]] (as it should be configured before the rest of Cloudbox is installed). 


Choose one of the following:

- [[Master Branch (default)|Install: Preinstall (Master Branch)]]  If you don't know which one to choose, use this one.
- [[Develop Branch|Install: Preinstall (Develop Branch)]]
