# lxc-cheatsheet
Lxc cheatsheet

## Debugging
1. Attaching only to the networking namespace (if for example we don't have nettols installed and want to use the system ones)

```sh
 sudo lxc-attach -s NETWORK -n tb-rugl-1603361435-6wvmi2lu2fkfwhsx3mq5snb6v4 -- iptables -nvLn
```

# lxd cheatsheet
WARNING: lxd is not needed for lxc. 
The lxd command is provided by lxd, no lxc:

```sh
$ sudo dpkg -S /usr/bin/lxc
lxd: /usr/bin/lxc
```
## Images
1. List image repos:

  ```sh
  lxc remote list
  ```
2. Search for remote images:

  ```sh
  lxc image list images: debian
  ```


## Running containers
1. Pull image and run container:

  ```sh
  sudo lxc launch ubuntu:20.04 ubuntuone
  ```
## Cleanup
List containers

```sh
sudo lxc list
+-----------+---------+----------------------+-----------------------------------------------+-----------+-----------+
|   NAME    |  STATE  |         IPV4         |                     IPV6                      |   TYPE    | SNAPSHOTS |
+-----------+---------+----------------------+-----------------------------------------------+-----------+-----------+
| ubuntuone | RUNNING | 10.245.252.15 (eth0) | fd42:ca75:8599:b882:216:3eff:fe71:5975 (eth0) | CONTAINER | 0         |
+-----------+---------+----------------------+-----------------------------------------------+-----------+-----------+

```
Delete containers

```sh
$ sudo lxc stop ubuntuone
$ sudo lxc delete ubuntuone

```
List images


```sh
sudo lxc image list
+-------+--------------+--------+---------------------------------------------+--------------+-----------+----------+-------------------------------+
| ALIAS | FINGERPRINT  | PUBLIC |                 DESCRIPTION                 | ARCHITECTURE |   TYPE    |   SIZE   |          UPLOAD DATE          |
+-------+--------------+--------+---------------------------------------------+--------------+-----------+----------+-------------------------------+
|       | e81943d40915 | no     | ubuntu 20.04 LTS amd64 (release) (20201014) | x86_64       | CONTAINER | 357.24MB | Oct 26, 2020 at 10:13am (UTC) |
+-------+--------------+--------+---------------------------------------------+--------------+-----------+----------+-------------------------------+
```
Delete images


```sh
sudo lxc image delete e81943d40915
```
List storage


```sh
sudo lxc storage list
+---------+-------------+--------+--------------------------------------------+---------+
|  NAME   | DESCRIPTION | DRIVER |                   SOURCE                   | USED BY |
+---------+-------------+--------+--------------------------------------------+---------+
| default |             | zfs    | /var/snap/lxd/common/lxd/disks/default.img | 1       |
+---------+-------------+--------+--------------------------------------------+---------+

```
Delete storage
Note that the storage associated to the default profile cannot be easily deleted ( https://stackoverflow.com/questions/42678979/how-to-remove-default-lxd-storage ) - not sure how badly this could mess up lxd.

```sh
sudo lxc storage list
[...]
sudo lxc storage delete <id>
```
