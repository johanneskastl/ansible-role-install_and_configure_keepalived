![Ansible Lint](https://github.com/johanneskastl/ansible-role-install_and_configure_keepalived/workflows/Ansible%20Lint/badge.svg)

install_and_configure_keepalived
=========

Install and configure keepalived

Requirements
------------

You need to have access to one (or more) IP address that you can (and are allowed to!) use. Depending on your environment, these addresses might need to be allowed on your machine (e.g. OpenStack has a concept of 'allowed IP addresses' that are allowed to be run on your VM in addition to the regular ones).

Role Variables
--------------

None.

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
