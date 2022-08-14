ansible-role-mikrotik
====

Configures MikroTik routers.

Requirements
------------

* [ansible-pylibssh](https://pypi.org/project/ansible-pylibssh/)

Role Variables
--------------

* `mikrotik_certs` - list of certificates to copy and import, example:
```yaml
mikrotik_certs:
  - src: myserver.crt
    dest: myserver.crt
  - src: myserver.key
    dest: myserver.key
    passphrase: verysecure
```
* `mikrotik_ip_services` - list of ip services to set, example:
```yaml
mikrotik_ip_services:
  - name: www-ssl
    options: certificate=myserver tls-version=only-1.2 disabled=no
  - name: www
    options: disabled=yes
```
* `mikrotik_dhcp_server_leases` - list of DHCP server leases, example:
```yaml
mikrotik_dhcp_server_leases:
  - address: 192.168.1.2
    mac_address: 70:85:C2:A9:B2:F7
    comment: myserver
```

Dependencies
------------

Collections:

* `ansible.netcommon`
* `community.routeros`


Example Playbook
----------------

```yaml
- hosts: mikrotik
  gather_facts: false
  vars:
    ansible_connection: ansible.netcommon.network_cli
    ansible_network_os: community.routeros.routeros
    ansible_user: admin
    ansible_password: verysecure
  roles:
    - ansible-role-mikrotik
```

License
-------

GPLv3

Author Information
------------------

Vladimir Vasilev (@vladi-k)
