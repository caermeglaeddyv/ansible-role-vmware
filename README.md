ReaR
=========

This role is used to manipulate resources in VMware vCenter, currently support creation of virtual machine(s) from scratch, from template, adding extra disk(s) to virtual machines, snapshotting them and controlling their powerstate.


Requirements
------------

This is not strict requirements and it may not work with other versions than tested ones.
Anyway. feel yourself free to test by yourself, suggest addition of new functionality and contribute.

Role is tested with:
- Ansible version >= 2.8.6
- VMware vCenter version = 6.7


Role Variables
--------------

```bash

# vCenter host/dns name or ip address:
vmware_hostname: ""

# vCenter username:
vmware_username: ""

# vCenter password:
vmware_password: ""

# Deploy virtual machine(s) from scratch (see documentation of module used at
# https://docs.ansible.com/ansible/latest/modules/vmware_guest_module.html
# and read defaults/main.yml and tasks/main.yml files for further information):
vmware_vm_from_scratch:
- name: ""
  guest_id: ""
  esxi_hostname: ""
  datastore: ""
  datacenter: ""
  folder: ""
  validate_certs: 
  state: ""
  hardware:
    num_cpus: 
    num_cpu_cores_per_socket: 
    cpu_limit: 
    hotadd_cpu: 
    memory_mb: 
    mem_limit: 
    hotadd_memory: 
    max_connections: 
  networks: 
  - name: ""
    vlan: 
    device_type: ""
    dvswitch_name: ""
    start_connected: 
    state: ""
  disk:
  - size_gb: ""
    type: ""

# Deploy virtual machine(s) from template (see documentation of module used at
# https://docs.ansible.com/ansible/latest/modules/vmware_guest_module.html
# and read defaults/main.yml and tasks/main.yml files for further information):
vmware_vm_from_template:
- name: ""
  esxi_hostname: ""
  datastore: ""
  datacenter: ""
  folder: ""
  template: ""
  validate_certs: 
  state: ""
  hardware:
    num_cpus: 
    num_cpu_cores_per_socket: 
    cpu_limit: 
    hotadd_cpu: 
    memory_mb: 
    mem_limit: 
    hotadd_memory: 
    max_connections: 
  networks:
  - name: ""
    vlan: 
    device_type: ""
    dvswitch_name: ""
    start_connected: 
    type: ""
    ip: 
    netmask: 
    gateway: 
    state: ""  
  customization:
    dns_servers:
    - ""

# Deploy extra disk(s) to virtual machine(s) (see documentation of module used at
# https://docs.ansible.com/ansible/latest/modules/vmware_guest_disk_module.html
# and read defaults/main.yml and tasks/main.yml files for further information):
vmware_extra_disk:
- name: ""
  datacenter: ""
  folder: ""
  validate_certs: 
  disk:
  - size_gb: 
    type: ""
    datastore: ""
    scsi_controller: 
    unit_number: 
    state: ""

# Snapshot virtual machine(s) (see documentation of module used at
# https://docs.ansible.com/ansible/latest/modules/vmware_guest_snapshot_module.html
# and read defaults/main.yml and tasks/main.yml files for further information):
vmware_snapshot:
- name: ""
  datacenter: ""
  folder: ""
  validate_certs: 
  state: ""
  snapshot_name: ""
  description: ""

# Change powerstate of virtual machine(s) (see documentation of module used at
# https://docs.ansible.com/ansible/latest/modules/vmware_guest_powerstate_module.html
# and read defaults/main.yml and tasks/main.yml files for further information):
vmware_powerstate:
- name: ""
  validate_certs: ""
  state: ""

```


Dependencies
------------

none


Example Playbook
----------------

```bash
---
- hosts: localhost
  gather_facts: false
  become: no
  tasks:
  - name: Check ansible version >=2.8.6
    assert:
      msg: Ansible must be v2.8.6 or higher
      that:
      - ansible_version.string is version("2.8.6", ">=")
    tags:
    - check
  vars:
    ansible_connection: local

- hosts: localhost
  tasks:
  - import_role:
      name: vmware
```

More detailed examples ( inventories, playbooks etc. ) of this and other roles can be found [here](https://github.com/caermeglaeddyv/examples/tree/dev/ansible).



License
-------

[Apache 2.0](https://github.com/caermeglaeddyv/ansible-role-vmware/blob/dev/LICENSE)


Author Information
------------------

Copyright 2020 [caermeglaeddyv](https://github.com/caermeglaeddyv)
