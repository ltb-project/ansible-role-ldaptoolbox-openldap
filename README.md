OpenLDAP
========

Ansible role which installs and configures [LTP-Projects](https://ltb-project.org/)'s OpenLDAP.

Requirements
------------

n/a

Role Variables
--------------

You'll need to store the hash value for you admin password. You'll get it like this:

```
/usr/local/openldap/sbin/slappasswd -o module-path="/usr/local/openldap/libexec/openldap" -o module-load="argon2" -h "{ARGON2}" -s "password"
```

Dependencies
------------


Example Playbook
----------------

Install and configure OpenLDAP on your servers:

    - hosts: openldap_servers
      roles:
         - ldaptoolbox.openldap

License
-------

GPLv3

Author Information
------------------

- Mathieu Jourdan
- David Coutadeur
