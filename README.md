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
    values: certificate=myserver tls-version=only-1.2 disabled=no
  - name: www
    values: disabled=yes
```
* `mikrotik_ip_pools` - list of IP pools, example:
```yaml
mikrotik_ip_pools:
  - key_name: name
    key_value: dhcp
    other_values: ranges=192.168.1.100-192.168.1.254
```
* `mikrotik_ip_dhcp_server_leases` - list of DHCP server leases, example:
```yaml
mikrotik_ip_dhcp_server_leases:
  - key_name: mac-address
    key_value: 70:85:C2:A9:B2:FF
    other_values: address=192.168.1.2 comment=myserver
```
* `mikrotik_ip_dns_statics` - list of static IP DNS records, example:
```yaml
mikrotik_ip_dns_statics:
  - key_name: name
    key_value: www.myserver.com
    other_values: address=192.168.1.2
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
