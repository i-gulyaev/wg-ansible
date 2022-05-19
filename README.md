# Ansible Scripts for VPN Server Bootstrap

This repository contains `ansible` scripts that help bootstrapping your own Wireguard VPN server.


## Usage
Define following variables in `vars/private.yml` (create this file if needed, see `vars/default.yml` as example).
- `admin_username`: VPS user with administrative privileges.
- `admin_password`: hashed sudo password for VPS admin (see [this](https://docs.ansible.com/ansible/latest/reference_appendices/faq.html#how-do-i-generate-encrypted-passwords-for-the-user-module) for details).
- `public_key`: path to a public SSH key used to provide password-less access to host for `admin_username`.
- `vpn_peers`: comma separated list of VPN peers to be configured by Wireguard (e.g. "mylaptop,myphone").

### Initial Server Bootstrap

The `bootstrap_vps.yml` script creates an admin user for the specified server and enables firewall and configures SSH access to the server.

```
ansible-playbook -l hostname -u root --ask-pass boostrap_vps.yml
```

### Setup Wireguard Server
The `setup_wireguard.yml` script installs docker infrastructure, pulls and brings up docker image with Wireguard server.
Wireguard peer configuration is populated at image start.

```
ansible-playbook -u vpsadmin setup_wireguard.yml
```

## Requirements

- Ubuntu 20.04 LTS
