# Stratiform
`stratiform` is an Ansible playbook for provisioning, configuring, and managing DigitalOcean droplets.

# Setup
This playbook requires the `community.digitalocean` collection. To install it via `ansible-galaxy`, run the following command:

`ansible-galaxy install -r requirements.yml`

For further documentation on the `community.digitalocean` collection, see the official docs on [Ansible Galaxy](https://docs.ansible.com/ansible/latest/collections/community/digitalocean/digital_ocean_droplet_module.html)

# Usage

## Hosts
Hosts in this playbook are not static, and are registered by the `do_droplet` role into the dynamic inventory.

## Group Vars

`./group_vars/all` is the main configuration source for this playbook. Any variables you need to update can be found there. Please do not update or change the role variables or edit the tasks or `site.yml` directly.

## Special Variables

In order to provision a new droplet, you must provide your DigitalOcean OAuth/API Token, along with at least one SSH key fingerprint from your DigitalOcean account.

These values should never be checked in as code, thus the best way to pass them is at runtime as a JSON object, with the SSH key fingerprints passed as a list element. The exact syntax can be found below.

## Droplet Sizes

DigitalOcean's API refers to their various droplet sizes using a slug. Valid droplet size slugs are as follows:

### Dedicated CPU Droplets

- - -
| General Purpose | CPU-Optimized | Memory-Optimized | Storage-Optimized |
| :-------------: | :-----------: | :--------------: | :---------------: |
| `g-2vcpu-8gb`   | `c-2`         | `m-2vcpu-16gb`   | `so-2vcpu-16gb`   |
| `g-4vcpu-16gb`  | `c-4`         | `m-4vcpu-32gb`   | `so1_5-2vcpu-16gb`|
| `gd-2vcpu-8gb`  | `c2-2vcpu-4gb`| `m3-2vcpu-16gb`  |                   |
| `gd-4vcpu-16gb` | `c2-4vcpu-8gb`| `m6-2vcpu-16gb`  |                   |
- - -

### Shared CPU
- - -
|   Sizes        |
|:--------------:|
| `s-1vcpu-2gb`  |
| `s-2vcpu-2gb`  |
| `s-2vcpu-4gb`  |
| `s-4vcpu-8gb`  |
| `s-8vcpu-16gb` |
- - -

## Droplet Images

> **NOTE:** _This is only a list of slugs for standard images. For a list of One-Click Application images, consult the official API docs, or use the following [`doctl`](https://github.com/digitalocean/doctl) command:_
>
> `doctl compute image list-application`

- - -
| Image Slug            | Image OS/Version                      |
|:---------------------:|:-------------------------------------:|
| `centos-7-x64`        | CentOS 7 (64-bit)                     |
| `centos-8-x64`        | CentOS 8 (64-bit)                     |
| `debian-9-x64`        | Debian 9 (64-bit)                     |
| `debian-10-x64`       | Debian 10 (64-bit)                    |
| `fedora-32-x64`       | Fedora 32 (64-bit)                    |
| `fedora-33-x64`       | Fedora 33 (64-bit)                    |
| `fedora-34-x64`       | Fedora 34 (64-bit)                    |
| `freebsd-11-x64-zfs`  | FreeBSD 11 (64-bit) w/ZFS Support     |
| `freebsd-11-x64-ufs`  | FreeBSD 11 (64-bit) w/UFS Support     |
| `freebsd-12-x64-ufs`  | FreeBSD 12 (64-bit) w/ZFS Support     |
| `freebsd-12-x64-zfs`  | FreeBSD 12 (64-bit) w/UFS Support     |
| `rancheros`           | RancherOS 1.5.8 (64-bit)              |
| `ubuntu-16-04-x32`    | Ubuntu 16.04 LTS (32-bit)             |
| `ubuntu-16-04-x64`    | Ubuntu 16.04 LTS (64-bit)             |
| `ubuntu-18-04-x64`    | Ubuntu 18.04 LTS (64-bit)             |
| `ubuntu-20-04-x64`    | Ubuntu 20.04 LTS (64-bit)             |
| `ubuntu-20-10-x64`    | Ubuntu 20.10 (64-bit)                 |
| `ubuntu-21-10-x64`    | Ubuntu 21.10 (64-bit)                 |
- - -

## Playbook
To run the playbook and set up droplets, run the following command:

`ansible-playbook -e "{'do_api_key':'<your_digitalocean_api_key>','do_ssh_key_fingerprints':['00:de:ad:be:ef:88:ab:cd:ef:12:34:56:78:00:aa:bb','...']}" site.yml`

> **NOTE:** _To get your SSH Key Fingerprint, run the following command:_
>
>`ssh-keygen -E md5 -lf ~/.ssh/id_rsa | cut -d' ' -f2 | sed s/MD5\://g`
