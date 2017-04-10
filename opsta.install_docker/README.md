Install Docker
=========

Ansible role to install Docker and do some initial configuration for Ubuntu host
- Install Docker
- Add ssh user to group docker
- Configure DOCKER_OPTS
- Login to private docker registry
- Install docker-py

You can see example how to make playbook, configuration and sample commands here https://github.com/winggundamth/ansible-wing-playbook

Requirements
------------

NA

Role Variables
--------------

```yaml
# This is default variables
install_docker_option: --storage-driver=overlay
install_docker_private_login: false
install_docker_py: false

# This is optional variables
# Use when install_docker_private_login is true
install_docker_registry_username: registry
install_docker_registry_password: CHANGEDOCKERPASSWORDHERE
install_docker_registry_email: docker@example.com
install_docker_registry_url: registry.example.com
```

Dependencies
------------

NA

Example Playbook
----------------

```yaml
- hosts: all
  gather_facts: no
  become: true
  roles:
    - winggundamth.install_docker
  vars_files:
    - "{{ install_docker_vars_file }}"
```

List of useful tags
----------------

There are some useful tags that you can use to maintain Docker configuration

- install-docker-private-login
- install-docker-configure
- install-docker
- install-docker-py

License
-------

MIT

Author Information
------------------

You can see my works at https://github.com/winggundamth
