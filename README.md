OpenLDAP
========

Ansible role which installs and configures [LTB-Project](https://ltb-project.org/)'s OpenLDAP.

Requirements
------------

- ansible
- HTTP connection to the LTB-project's repository

Role Variables
--------------

You'll need to store the hash value for you admin passwords. You'll get it like this:

```
/usr/local/openldap/sbin/slappasswd -o module-path="/usr/local/openldap/libexec/openldap" -o module-load="argon2" -h "{ARGON2}" -s "password"
```

Store the passwords in the vault file in: `tests/credentials-vault.yml`


Playbook examples
-----------------

You should:
 * either deploy your role
 * or use a configuration file for setting the role path, for example:

ansible.cfg
```
[defaults]
roles_path=../
```

See `tests/standalone.yml`

Run playbook with:

```
ansible-playbook tests/standalone.yml -i tests/inventory --ask-vault-pass
```

or:

```
ansible-playbook tests/standalone.yml -i tests/inventory --vault-password-file .vault_pass
```

If you need a two-nodes multimaster example, give a look at `tests/multimaster1.yml` and `tests/multimaster2.yml`


License
-------

GPLv3

Author Information
------------------

- Mathieu Jourdan
- David Coutadeur
