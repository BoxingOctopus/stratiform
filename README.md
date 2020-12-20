# Stratiform
`stratiform` is an Ansible playbook for provisioning, configuring, and managing DigitalOcean droplets.

# Setup
This playbook requires the `community.digitalocean` collection. To install it via `ansible-galaxy`, run the following command:

`ansible-galaxy install -r requirements.yml`

# Usage

## Hosts
Hosts in this playbook are not static, and are registered by the `do_droplet` role into the dynamic inventory.

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
| `gd-4vcpu-16gb` | `c2-4vpcu-8gb`| `m6-2vcpu-16gb`  |                   |
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

## Playbook
To run the playbook and set up droplets, run the following command:

`ansible-playbook -e "{'do_api_key':'<your_digitalocean_api_key>','do_ssh_key_fingerprints':['00:de:ad:be:ef:88:ab:cd:ef:12:34:56:78:00:aa:bb','...']}" site.yml`
