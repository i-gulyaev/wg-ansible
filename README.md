# Ansible Scripts for VPN Server Bootstrap

This repository contains `ansible` scripts that help bootstrapping your own Wireguard VPN server packaged as a docker container.

More info here: https://docs.linuxserver.io/images/docker-wireguard/

## Usage
Define following variables in `vars/private.yml` (create this file if needed, use `vars/default.yml` as example).
- `admin_username`: VPS user with administrative privileges.
- `admin_password`: hashed sudo password for VPS admin (see [this](https://docs.ansible.com/ansible/latest/reference_appendices/faq.html#how-do-i-generate-encrypted-passwords-for-the-user-module) for details).
- `public_key`: path to a public SSH key used to provide password-less access to host for `admin_username`.
- `vpn_peers`: comma separated list of VPN peers to be configured by Wireguard (e.g. "mylaptop,myphone").

### Initial Server Bootstrap

1. Add new server to `hosts.yaml`.

```
vpn:
  hosts:
    new-server:
      ansible_host: 10.20.30.40
      vpn_host: 10.20.30.40
      vpn_port: 51820
```
2. Run `bootstrap_vps.yml` script.
It creats an admin user for the specified server and enables firewall and configures SSH access to the server.

```
ansible-playbook -l new-server -u root --ask-pass bootstrap_vps.yml
```

### Setup Wireguard Server
The `setup_wireguard.yml` script installs docker infrastructure, pulls and brings up docker image with Wireguard server.
Wireguard peer configuration is populated at image start.

```
ansible-playbook -u vpsadmin setup_wireguard.yml
```

## Requirements

- Ubuntu 20.04 LTS
