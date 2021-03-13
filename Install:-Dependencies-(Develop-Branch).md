Here you will install the Dependencies and download the Cloudbox Repository.

_Note: You can run the following commands from any path._

_Note: Source for Develop branch scripts can be found [here](https://github.com/Cloudbox/cb/tree/develop)._

_There are a lot of changes are going on in the develop branch and things are being ironed out as I get around to fixing them. So I would recommend that users avoid switching to Dev branch for now, unless there are willing to deal with occasional oddities, quirks, and bugs. Consider current develop branch an alpha build rather than a beta one._

Choose between [New Installs (Systems without CB)](#New-Install) **OR** [Master --> Develop Migration](#Develop-Migration) install steps.

## New Install

Use this method on a system which does not already have Cloudbox installed.

### 1) Install CB Scripts/Dependencies/CB Repo

Run the following command:


```
curl -s https://raw.githubusercontent.com/Cloudbox/cb/develop/cb_install.sh | sudo -H bash; cd /srv/git/cloudbox
```

<details>
  <summary>Click for an alternative that uses wget [an alternative to curl].</summary>
  <br />

```
wget -qO- https://raw.githubusercontent.com/Cloudbox/cb/develop/cb_install.sh | sudo -H bash; cd /srv/git/cloudbox
```
</details>

Cloudbox will clone to `/srv/git/cloudbox`.

### 1A) DO NOT JUMP TO STEP TWO ON THIS PAGE

Carry on with your cloudbox install as per the wiki, up to the "Install Cloudbox/Mediabox/Feederbox" step then proceed to the next step on this page. If you skip those steps and install Cloudbox/Mediabox/Feederbox right now you will have problems. Creation of `.ansible_vault` will need to be done **after** you have created your user. If you use the preinstall role to create the user for you then you should do this step afterwards.

### 2) Install Cloudbox/Mediabox/Feederbox (when you get to that step) with these instructions

**NOTE: You need to have completed steps 3-7 in the regular install before you do this.**

**NOTE: You should NOT be logged into your server as `root` at this point.  You should be logged in as the user you created/specified in the [[preinstall|Install: Preinstall]].**

```
cb install cloudbox
```

A symlink to `/srv/git/cloudbox` will be created at `~/cloudbox`.

_Need to be out of `~/cloudbox` folder for this._ 

### 3) CB Script Usage

You can now use `cb install <rolename>` to run Cloudbox roles from anywhere; you do not need to be in `~/cloudbox`.

---

## Develop Migration

Use these instructions to migrate an existing *master branch* Cloudbox system to the current *develop* branch.

<!--
```
curl -s https://raw.githubusercontent.com/Cloudbox/cb/develop/cb_install.sh | sudo -H bash; cd /srv/git/cloudbox
```

or

```
wget -qO- https://raw.githubusercontent.com/Cloudbox/cb/develop/cb_install.sh | sudo -H bash; cd /srv/git/cloudbox
```
-->
### 1) Pull latest changes

```
cd ~/cloudbox
git fetch
git reset --hard @{u}
git checkout develop
git reset --hard @{u}
```

Two resets to resolve potential merge conflicts and other git-related issues.

### 2) Update Ansible

```
sudo pip install 'ansible>=2.9,<2.10'
```

### 3) Cloudbox Folder Backup and CB Scripts Download

```
cd ~/cloudbox
sudo ansible-playbook cloudbox.yml --tags user
```
Cloudbox will cloned to `/srv/git/cloudbox` and your config files will be copied there as well.

_You can remove the backup folder (`~/cloudbox_REMOVE_ME`) if you choose._

### 4) Cloudbox Folder Symlink Creation

```
cd ~/
cb install user
```
A symlink to `/srv/git/cloudbox` will be created at `~/cloudbox`.

_Need to be out of `~/cloudbox` folder for this._ 

### 5) CB Script Usage

You can now use `cb install <rolename>` to run roles from anywhere.