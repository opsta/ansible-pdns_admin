Manage redis container
=========

Ansible role to install New Relic agent
- Install New Relic agent and configure with provided license key
- Add New Relic agent to docker group so it can monitor docker container

You can see example how to make playbook, configuration and sample commands here https://github.com/winggundamth/ansible-wing-playbook

Requirements
------------

- Ansible 2.0

Role Variables
--------------

```yaml
# This is default variables
newrelic_package_name: newrelic-sysmond
newrelic_service_name: newrelic-sysmond
newrelic_deb_repository: deb http://apt.newrelic.com/debian/ newrelic non-free
newrelic_apt_key_url: https://download.newrelic.com/548C16BF.gpg
newrelic_apt_key_id: 548C16BF
newrelic_run_user: newrelic
newrelic_docker_package_name: docker-engine
newrelis_docker_group: docker

# You have to change this
newrelic_license_key: CHANGEME
```

Dependencies
------------

N/A

Example Playbook
----------------

```yaml
- hosts: all
  gather_facts: no
  become: true
  roles:
    - winggundamth.newrelic
  vars_files:
    - "{{ newrelic_vars_file }}"
```

License
-------

MIT

Author Information
------------------

You can see my works at https://github.com/winggundamth
