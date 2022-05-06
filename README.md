![Ansible Lint](https://github.com/johanneskastl/ansible-role-install_and_configure_keepalived/workflows/Ansible%20Lint/badge.svg)

install_and_configure_keepalived
=========

This role installs and configures keepalived for **simple** scenarios. At this time it only supports one or more `vrrp_instance` blocks with the bare minimum of settings to get it working.

Please don't expect this role to support each and every configuration option that keepalived has...

Requirements
------------

You need to have access to one (or more) IP address that you can (and are allowed to!) use. Depending on your environment, these addresses might need to be allowed on your machine (e.g. OpenStack has a concept of 'allowed IP addresses' that are allowed to be run on your VM in addition to the regular ones).

Role Variables
--------------

## General system settings

Those should be pretty much the same on most Linux distributions:

- `systemd_unit_name`: name of the systemd service, defaults to `keepalived.service`
- `package_name`: name of the package to install, defaults to `keepalived`
- `config_file_path`: path to the keepalived configuration file, default is `/etc/keepalived/keepalived.conf`

## VRRP defaults

Those defaults are used for all vrrp_instance blocks, unless you specify them via the role variables you supply:

- `vrrp_advert_int`: (default: `1`)
- `vrrp_interface`: (default: `eth0`)

## VRRP variables that you need to provide

For each of the vrrp_instances you want to set up, you need to provide the following:

```
- name: 'VI_121'
  virtual_ip_addresses:
    - '192.168.121.121/24'
  priority:
    keepalived1: '255'
    keepalived2: '200'
  virtual_router_id: '121'
- name: 'VI_122'
```

The required variables that can be used are:

- `name`: name of this `vrrp_instance`
- `virtual_ip_addresses`: list of virtual IP addresses, that this `vrrp_instance` should handle
- `priority`: for each keepalived node, this variable contains a key-value-pair with the host's name as key and the priority as value

The optional variables are:

- `state`: you can set a `state` option on a vrrp_instance, to tell keepalived that this node is supposed to be the MASTER or BACKUP node. This let's the instance transition to this state immediately, if the `priority` is set accordingly (MASTER: 255, BACKUP: 200). This variable is expected to hold key-value-pairs for all of the nodes, with the host's name being the key and the `state` (i.e. `MASTER` or `BACKUP`) as the value

```
  state:
    keepalived1: 'MASTER'
    keepalived2: 'BACKUP'
```

In case you are using multicast, you need to specify the following variables:

- `virtual_router_id`: the ID used for this virtual router (if multicast is being used)

Dependencies
------------

None

Example Playbook
----------------

    - hosts: servers
      roles:
        - role: 'johanneskastl.install_and_configure_keepalived'

License
-------

BSD-3-Clause

Author Information
------------------

I am Johannes Kastl, reachable via kastl@b1-systems.de.
