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

