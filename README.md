OpenLDAP
========

Ansible role which installs and configures [LTB-Project](https://ltb-project.org/)'s OpenLDAP.

Requirements
------------

- ansible
- HTTP connection to the LTB-project's repository

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

See `tests/test.yml`

Run playbook with:

```
ansible-playbook tests/test.yml -i tests/inventory --ask-vault-pass
```

License
-------

GPLv3

Author Information
------------------

- Mathieu Jourdan
- David Coutadeur
