Install Docker Compose
=========

Ansible role to install Docker Compose on local machine

You can see example how to make playbook, configuration and sample commands here https://github.com/winggundamth/ansible-wing-playbook

Requirements
------------

NA

Role Variables
--------------

```yaml
# This is default variables
docker_compose_install_version: 1.7.1
docker_compose_install_url: https://github.com/docker/compose/releases/download/{{ docker_compose_install_version }}/docker-compose-{{ ansible_system }}-{{ ansible_architecture }}
docker_compose_install_path: /usr/local/bin/docker-compose
```

Dependencies
------------

NA

Example Playbook
----------------

```yaml
- hosts: localhost
  connection: local
  gather_facts: yes
  become: false
  roles:
    - role: winggundamth.docker_compose
  vars_files:
    - "{{ docker_compose_vars_file }}"
```

If your system need sudo password. You must use ```--ask-become-pass``` when running playbook.

License
-------

MIT

Author Information
------------------

You can see my works at https://github.com/winggundamth
