# Ansible role: local-users

Ansible role for user and groups management. Currently this works on Debian and RedHat based linux systems. Tested platforms are:

* Ubuntu 16.04
* Ubuntu 14.04
* Debian 9
* Debian 8
* CentOS 7
* CentOS 6

Requirements
------------

None

Role Variables
--------------

The variables that can be passed to this role and a brief description about them are as follows. (For all variables, take a look at defaults/main.yml)

```yaml
# groups
user_groups:
  - name: group01
    uid: 1100
    state: present
  - name: group02
    state: present

user_list:
  - name: admin
    uid: 1001
    comment: "Big Admin"
    password: "place for sha512 hash"
    key_file: "key/key_admin.pub"
    group: admin
    groups: [ "group01", "group02" ]
    state: present
  - name: user
    group: user
    groups: [ "group01" ]
    state: present

# If you use user_list in group variables and want to extra users for some hosts.
# You should describe extra_user_list in host_variables
extra_user_list:
  - name: extra_user
    group: user
    groups: [ "group01" ]
    state: present

sudo_users:
  - name: ansible_sudo
    user: "%group01"
    host: ALL
    runas: ALL
    tag: NOPASSWD
    cmd: ALL
```

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: app
  roles:
      - mbaran0v.local-users
```

License
-------

MIT / BSD

Author Information
------------------

This role was created in 2018 by Maxim Baranov.
