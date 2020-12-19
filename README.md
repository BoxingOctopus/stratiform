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

## Vault secrets
All playbook-wide secrets are kept in a vault under `./group_vars/vault_vars`. To unlock the vault, place a file with the vault password in `./.vault_pass` and
run the following command:

`ansible-vault decrypt --vault-password-file .vault_pass ./group_vars/vault_vars`

**NOTE:** _Take care not to leave vaults decrypted when you check new code into the repo. It may be helpful to use the included pre-commit hook (`./utils/vault-pre-commit-hook.sh`) to prevent this from happening._

## Playbook
To run the playbook and set up droplets, run the following command:

`ansible-playbook -i hosts site.yml`
