# ansible-jupyterhub

Ansible role and playbooks to install JupyterHub on a server, and manage users.

This repo will be used with other repos to create a full management system for JuptyerHub, see [Website](https://github.com/Cassiopee-Bureau-Mobile/website)

## Features

- Install JupyterHub
- Add user with username and password
- Change user password
- Delete user
- Restart JupyterHub

# Quickstart

You can use the sample inventory file to have a quick start in local.

For production, you must fill the cassiopee inventory file with your own configuration.

## Install JupyterHub

```bash
ansible-playbook playbooks/install.yml -i inventories/cassiopee/hosts.ini
```

This will install JupyterHub on the server. You can then access it at `https://<server_ip>/`.

Here is the default configuration:

```yaml
load_firewall_rules: true

openvpn_server_ip: # IP of the OpenVPN server
ip_range: # IP range to restrict ssh access to the server

notebook_runner_git_url: https://github.com/Cassiopee-Bureau-Mobile/Notebook-Runner
```

When testing locally, you can set `load_firewall_rules` to `false` to avoid messing with your firewall.

## Add user

```bash
ansible-playbook playbooks/add_user.yml -i inventories/cassiopee/hosts.ini --extra-vars "username=<username> password=<password>"
```

This will add a user to the server. The user will be able to access JupyterHub at `https://<server_ip>/user/<username>/`.

## Change user password

```bash
ansible-playbook playbooks/change_password.yml -i inventories/cassiopee/hosts.ini --extra-vars "username=<username> password=<password>"
```

This will change the password of a user.

## Delete user

```bash
ansible-playbook playbooks/delete_user.yml -i inventories/cassiopee/hosts.ini --extra-vars "username=<username>"
```

This will delete a user from the server. The user will no longer be able to access JupyterHub. The user's home directory will be deleted.

## Restart JupyterHub

```bash
ansible-playbook playbooks/restart.yml -i inventories/cassiopee/hosts.ini
```

This will restart JupyterHub service.

# Configuration

## Inventory

You can use the `inventories/sample/hosts.ini` file as an example to create your own inventory file.

You can switch to ssh key authentication by setting `ansible_ssh_private_key_file` in the inventory file.
