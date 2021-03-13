Here you will install the Dependencies and download the Cloudbox Repository.

_Note: You can run the following commands from any path._

_Note: Source for the scripts can be found [here](https://github.com/Cloudbox/cloudbox.github.io/tree/master/scripts)._

Choose either [Combined](#Combined) or [Separated](#Separated) install steps.

If you don't know which one to choose, choose the first option under the [Combined](#Combined) heading.

## Combined 

Install Dependencies and GitHub Repo in one command.

Run the following command:

```
curl -s https://cloudbox.works/scripts/dep.sh | sudo -H bash; curl -s https://cloudbox.works/scripts/repo.sh | bash >/dev/null 2>&1; cd ~/cloudbox
```

<details>
  <summary>Click for an alternative that uses wget [an alternative to curl].</summary>
  <br />

  ```
  wget -qO- https://cloudbox.works/scripts/dep.sh | sudo -H bash; wget -qO- https://cloudbox.works/scripts/repo.sh | bash >/dev/null 2>&1; cd ~/cloudbox
  ```
</details>

---

## Separated 

Install Dependencies and GitHub Repo in two commands.


### 1. Install Dependencies

Run the following command:

```
curl -s https://cloudbox.works/scripts/dep.sh | sudo -H sh
```

<details>
  <summary>Click for an alternative that uses wget [an alternative to curl].</summary>
    <br />

```
wget -qO- https://cloudbox.works/scripts/dep.sh | sudo -H sh
```
</details>

**Ansible Version Installed: `2.5.14`** 

### 2. Download Cloudbox Repository

Run the following command:

```
curl -s https://cloudbox.works/scripts/repo.sh | bash >/dev/null 2>&1; cd ~/cloudbox
```

<details>
  <summary>Click for an alternative that uses wget [an alternative to curl].</summary>
  <br />

```
wget -qO- https://cloudbox.works/scripts/repo.sh | bash >/dev/null 2>&1; cd ~/cloudbox
```
</details>


<details>
  <summary>Click if that command fails to copy config files into the `~/cloudbox` folder.</summary>
  <br />

Run the following command:
  
```
git clone --recursive https://github.com/cloudbox/cloudbox.git ~/cloudbox; cd ~/cloudbox && cp -n defaults/ansible.cfg.default ansible.cfg; cp -n defaults/accounts.yml.default accounts.yml; cp -n defaults/settings.yml.default settings.yml; cp -n defaults/adv_settings.yml.default adv_settings.yml
```
</details>

