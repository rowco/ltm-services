Ansible role to configure basic LTM services on BIGIP

Basic concepts:
  - Virtual Servers are managed as Ansible 'hosts', each one needs an entry in the inventory.
  - Each Virtual Server consists of one Virtual Server, one Pool with members, and optionally ssl keys and certificates.
  - Virtual Servers have their configuration stored as host_vars, with defaults from group_vars then role defaults.


Requires 'hash_behaviour=merge' in ansible.cfg


Example inventory

```
[ltm_services]
f5-vip-a.demo
f5-vip-b.demo
```

Example host_vars

host_vars/f5-vip-a.demo

```
f5_server: bigip-1.demo
virtual_address: "1.1.1.1"
port: "443"
partition: "Common"
ssl: true
ssl_cert_name: "f5-vip-a.demo"
nodes:
  - host: "2.2.2.1"
  - host: "2.2.2.2"
```


host_vars/f5-vip-b.demo

```
f5_server: bigip-1.demo
virtual_address: "1.1.1.2"
port: "443"
partition: "Common"
ssl: true
ssl_cert_name: "f5-vip-b.demo"

nodes:
  - host: "3.3.3.1"
  - host: "3.3.3.2"

bigip_virtual_server:
  description: "Demo service"
  profiles:
    - "http"
    - "serverssl"
    - "{{inventory_hostname}}_client_ssl"

bigip_pool:
  lb_method: "least-connections-node"
  monitors:
    - "http"
```
