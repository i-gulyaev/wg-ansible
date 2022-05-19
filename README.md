# Ansible Scripts for VPN Server Bootstrap

This repository conntains `ansible` scripts that help bootstrapping you own Wireguard VPN server.


## Usage

### Setup User

The `setup_admin_user.yml` script creates an admin user on the specified server.

```
ansible-playbook -l hostname -u root --ask-pass setup_admin_user.yml
```

### Setup Wireguard VPN Server
