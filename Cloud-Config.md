# Cloud-Config

Can use this to create new user accounts (e.g. Hetzner Cloud). 

## Password Login (Less Secure)


`passwd` hash: 

```
mkpasswd --method=SHA-512 --rounds=4096
```


```yaml
#cloud-config

groups:
  - docker

users:
  - name: seed
    sudo: ALL=(ALL) NOPASSWD:ALL
    groups: sudo, docker
    ssh_import_id: foobar
    lock_passwd: false
    passwd: $6$rounds=4096$a/9BYJmHI1c0KhYi$zKHWPZzynckUSzS3lLCjpvjhRR.nn.ManqqPDo4OnjFMmXMfAfhopHb8sv9AtsOFQEYu4k4m.eT90HuT2oO.P1
```

## SSH Key Login (More Secure)


(replace `<ssh pub key 1>` with your ssh pub key)

```yaml
#cloud-config

groups:
  - docker

users:
  - name: seed
    sudo: ALL=(ALL) NOPASSWD:ALL
    groups: sudo, docker
    ssh_authorized_keys:
      - <ssh pub key 1>
```