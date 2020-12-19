# Stratiform
`stratiform` is an Ansible playbook for provisioning, configuring, and managing DigitalOcean droplets.

# Setup
This playbook requires the `community.digitalocean` collection. To install it via `ansible-galaxy`, run the following command:

`ansible-galaxy install -r requirements.yml`

# Usage

## Hosts
Hosts can be found in the `./hosts` file.

## Variables
* Playbook-wide vars can be found in `./group_vars`.
* Droplet-specific vars can be found in `./host_vars`.

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

## Vault secrets
All playbook-wide secrets are kept in a vault under `./group_vars/vault_vars`. To unlock the vault, place a file with the vault password in `./.vault_pass` and
run the following command:

`ansible-vault decrypt --vault-password-file .vault_pass ./group_vars/vault_vars`

**NOTE:** _Take care not to leave vaults decrypted when you check new code into the repo. It may be helpful to use the included pre-commit hook (`./utils/vault-pre-commit-hook.sh`) to prevent this from happening._

## Playbook
To run the playbook and set up droplets, run the following command:

`ansible-playbook -i hosts site.yml`
