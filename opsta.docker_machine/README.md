Manage Docker Machine
=========

Ansible role to manage machines for Docker Machine.
- Install Docker Machine
- Docker Machine create to each target host in inventory
- Search and replace docker machine config.json file to change directory to where it stores

You can see example how to make playbook, configuration and sample commands here https://github.com/winggundamth/ansible-wing-playbook

Remarks
------------

- This role will run docker-machine command on local machine
- The target machine name in inventory file will be the name of machine name in ```docker-machine ls```
- Default Docker Machine storage path will be at ```files/docker-machine``` of the playbook. You can change it via ```docker_machine_storage_path``` variable
- This role intends to be conditional role so in playbook you need to configure variable to specific task to run. You can see example in [Example Playbook](#Example-Playbook) section
  - Set ```docker_machine_create``` variable to ```true``` to run docker-machine create
  - Set ```docker_machine_manage_config``` variable to ```true``` to search and replace docker machine config.json

Requirements
------------

- You must can ssh to target host with ssh key

Role Variables
--------------

```yaml
# This is default variables
docker_machine_create: false
docker_machine_manage_config: false
docker_machine_install_version: 0.7.0
docker_machine_install_url: https://github.com/docker/machine/releases/download/v{{ docker_machine_install_version }}/docker-machine-{{ ansible_system }}-{{ ansible_architecture }}
docker_machine_install_path: /usr/local/bin/docker-machine
docker_machine_install_checksum: md5:bf73bbfee97fad04d3ff20151b1847fa
docker_machine_storage_path: "{{ playbook_dir }}/files/docker-machine"
docker_machine_config_file: "{{ docker_machine_storage_path }}/machines/{{ inventory_hostname }}/config.json"
docker_machine_config_variables:
  - { regexp: '"StorePath": "(.*)",$', replace: '"StorePath": "{{ docker_machine_storage_path }}",' }
  - { regexp: '"StorePath": "(.*)"$', replace: '"StorePath": "{{ docker_machine_storage_path }}/machines/{{ inventory_hostname }}"' }
  - { regexp: '"CertDir": "(.*)",$', replace: '"CertDir": "{{ docker_machine_storage_path }}/certs",' }
  - { regexp: '"CaCertPath": "(.*)",$', replace: '"CaCertPath": "{{ docker_machine_storage_path }}/certs/ca.pem",' }
  - { regexp: '"CaPrivateKeyPath": "(.*)",$', replace: '"CaPrivateKeyPath": "{{ docker_machine_storage_path }}/certs/ca-key.pem",' }
  - { regexp: '"ServerCertPath": "(.*)",$', replace: '"ServerCertPath": "{{ docker_machine_storage_path }}/machines/{{ inventory_hostname }}/server.pem",' }
  - { regexp: '"ServerKeyPath": "(.*)",$', replace: '"ServerKeyPath": "{{ docker_machine_storage_path }}/machines/{{ inventory_hostname }}/server-key.pem",' }
  - { regexp: '"ClientKeyPath": "(.*)",$', replace: '"ClientKeyPath": "{{ docker_machine_storage_path }}/certs/key.pem",' }
  - { regexp: '"ClientCertPath": "(.*)",$', replace: '"ClientCertPath": "{{ docker_machine_storage_path }}/certs/cert.pem",' }

# This is optional variables
docker_machine_extra_parameters: --engine-registry-mirror https://registry-mirror.example.com
```

Dependencies
------------

NA

Example Playbook
----------------

```yaml
- hosts: all
  connection: local
  gather_facts: yes
  become: false
  roles:
    - role: winggundamth.docker_machine
      docker_machine_create: true
      docker_machine_manage_config: true
  vars_files:
    - "{{ docker_machine_vars_file }}"
```

List of useful tags
----------------

There are some useful tags that you can use to maintain Docker Machine

- docker-machine-create (this needs to configure ```docker_machine_create``` variable to ```true```)
- docker-machine-install (this needs to configure ```docker_machine_create``` variable to ```true```)
- docker-machine-manage-config (this needs to configure ```docker_machine_manage_config``` variable to ```true```)

License
-------

MIT

Author Information
------------------

You can see my works at https://github.com/winggundamth
