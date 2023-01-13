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
* `mikrotik_ip_addresses` - list of IP addresses, example:
```yaml
mikrotik_ip_addresses:
  - key_name: interface
    key_value: bridge
    other_values: address=192.168.1.1/24
```
* `mikrotik_ip_dhcp_server_networks` - list of DHCP Server network options, example:
```yaml
mikrotik_ip_dhcp_server_networks:
  - key_name: comment
    key_value: defconf
    other_values: address=192.168.1.0/24 gateway=192.168.1.1 dns-server=192.168.1.1
```
* `mikrotik_ip_dhcp_clients` - list of DHCP clients, example:
```yaml
mikrotik_ip_dhcp_clients:
  - key_name: interface
    key_value: ether1
    other_values: add-default-route=yes use-peer-dns=no
```
* `mikrotik_ip_services` - list of IP services to set, example:
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
* `mikrotik_ip_dns` - configure IP DNS, example:
```yaml
mikrotik_ip_dns: use-doh-server=https://freedns.controld.com/p2 verify-doh-cert=yes allow-remote-requests=yes
```
* `mikrotik_interface_ovpn_clients` - configure OpenVPN client interface, example:
```yaml
mikrotik_interface_ovpn_clients:
  - key_name: name
    key_value: ovpn-client
    other_values: connect-to=vpn.acme.com port=1194 protocol=udp mode=ip profile=default certificate=mikrotik.crt_0 cipher=aes256 tls-version=only-1.2 use-peer-dns=no add-default-route=no user=mikrotik auth=sha256
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
