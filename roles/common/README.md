Common
=========

This is a simple setup role for a RHEL based system. It sets up the systems to be ready to access SSH commands, and to use sudo without a password. This is designed to be a base for other roles. Uses 'become' keyword for initial setup, so will require a password for initial setup.


Role Variables
--------------

- user
  - The username to use when setting up the user for sudoers and ssh on the systems
  - Default: rts-ansible

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

``` Ansible
- hosts: all
  roles:
    - role: common
      vars:
        - user: "someUserName"
```

License
-------

MIT

Author Information
------------------

[Lucas Roe](mailto:lroe@realtechnologysolutions.io)