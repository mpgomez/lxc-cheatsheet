# lxc-cheatsheet
Lxc cheatsheet

## Images
1. List image repos:

  ```sh
  lxc remote list
  ```
1. Search for remote images:

  ```sh
  lxc image list images: debian
  ```


## Running containers
1. Pull image and run container:

```sh
sudo lxc launch ubuntu:20.04 ubuntuone
```
