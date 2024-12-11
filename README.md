OpenLDAP
========

Ansible role which installs and configures [LTB-Project](https://ltb-project.org/)'s OpenLDAP on Debian and RHEL like targets.

Requirements
------------

- ansible
- ssh
- git if you get this role from the git repository
- HTTP connection to the LTB-project's repository

Targets OS supported : Debian and RHEL like from version 7.

Role Variables
--------------

You'll need to store the hash value for your admin passwords. You'll get it like this:

```
/usr/local/openldap/sbin/slappasswd -o module-path="/usr/local/openldap/libexec/openldap" -o module-load="argon2" -h "{ARGON2}" -s "password"
```

Store the passwords in the vault file in: `playbook/credentials-vault.yml`


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

See `playbook/standalone.yml`

Run playbook with:


```
ansible-playbook playbook/standalone.yml -i playbook/inventory --ask-vault-pass
```

You can also run an openldap cluster with 2 masters and 2 slaves with the multimaster playbook:

```
ansible-playbook playbook/multimaster.yml -i playbook/inventory --ask-vault-pass
```

or:

```
ansible-playbook playbook/multimaster.yml -i playbook/inventory --vault-password-file .vault_pass
```

For using this cluster, you must create the corresponding machines and declare the routes, as defined in `playbook/inventory`.

You also have to fill the certificate in `playbook/certificates-vault.yml`. You can use this command for editing the file: (the default password is: secret)

```
ansible-vault edit playbook/certificates-vault.yml
```

If you want the certificates to be deployed by ansible, you can enable it by adding this variable in your playbook:

```
ldaptoolbox_openldap_deploy_certificates: true
```

You can also configure the OpenLDAP version to install. Currently, only 2.5 and 2.6 are supported. The default is 2.6. You can change this in your playbook with:

```
ldaptoolbox_openldap_version: "2.5"
```


Give a look at `playbook/group_vars/prod.yml`, `playbook/host_vars/master1.yml` and `playbook/host_vars/master2.yml` for variable customization
You can also use `--extra-vars variable=value` at the command line for overloading any variable.


Give a look to `playbook/monitoring.yml` for an example of playbook that deploys LTB monitoring and statistics tools

Run the corresponding task with: 

```
ansible-playbook playbook/monitoring.yml -i playbook/inventory
```

Give a look to `playbook/sasl.yml` for an example of playbook that install and deploy sasl for OpenLDAP to delegate authentication to another directory.

Run the corresponding playbook with:

```
ansible-playbook playbook/sasl.yml -i playbook/inventory --vault-password-file .vault_pass
```

License
-------

GPLv3

Author Information
------------------

- Mathieu Jourdan
- David Coutadeur
