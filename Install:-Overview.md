Read through this entire setup process at least once before you begin.  There are several steps that all need to be completed before installation is complete.

Before you begin:
 1. Have you reviewed the [presumptions](https://github.com/Cloudbox/Cloudbox/wiki/Prerequisites%3A-Presumptions)?
 1. Do you have a [server](https://github.com/Cloudbox/Cloudbox/wiki/Prerequisites%3A-Server) that meets cloudbox' requirements?
 1. Have you set up your [domain](https://github.com/Cloudbox/Cloudbox/wiki/Prerequisites%3A-Domain-Name)?

Points regarding setup process:

- Installation does not require a previous account to be setup as **Step 5** (i.e [[Preinstall|Install: Preinstall]]), will create a user account for you. So you can start installing Cloudbox from a root account if you choose.

***

Note: **THERE IS NO AUTOMATED UNINSTALL**.  

The Cloudbox install process assumes you are installing on a brand new blank machine; it installs a variety of services and docker containers and makes tweaks to various OS-level configurations.  The list changes from time to time; there are also customizations that the user can perform or additional containers the user can install.  Because of this, an automated uninstall facility is not practical.  

If you want to remove all traces of Cloudbox, reformat the machine.  You can go through the code [or perhaps your install log] and "undo" everything the install does, but the preferred and suggested method is to reformat.
