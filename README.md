ansible-role-pdns_admin
=======================

Ansible role to install PowerDNS-Admin, a python-based webfrontend for PowerDNS.

Tested on Debian 10, 11 only!

Requirements
------------

None at the moment.

Description
-----------

There are two ways to install pdns-Admin - either natively (using git, yarn, etc.) or using docker.

The necessary variables differ - choose the table that fits your requirements

Role Variables
--------------

### Common variables

| Variable | Default | Comments (type) |
| --- | --- | --- |
| pdns_admin__install_mode | 'docker' | Either 'docker' or 'native'. Describes the install mode. |
| pdns_admin__listen_port | 9393 | The port pdns-admin should listen on. On docker, this is the port on the host that is forwarded to the container |
| pdns_admin__listen_ip | 127.0.0.1 | The port pdns-admin should listen on. On docker, this is the IP of the host that will forwarded to the container |
| pdns_admin__database_config | empty | The database config for pdns-admin (details below) **mandatory** |
| pdns_admin__database_credentials | empty | The credentials used to log in to the mysql host (for user & DB creation; details below) **mandatory** |

### Docker variables

| Variable | Default | Comments (type) |
| --- | --- | --- |
| pdns_admin__docker_packages | distro specific | A list of packages needed for docker |
| pdns_admin__docker_compose_dir | '/opt/docker-compose/pdns-admin' | The docker-compose dir where the config is stored |
| pdns_admin__image_name | 'ngoduykhanh/powerdns-admin' | The image location to use |
| pdns_admin__container_name | pdns-admin | The name for the docker container |

### schema of pdns_admin__database_config

| Key | Comments (type) |
| --- | --- |
| sqla_db_user | The database user for pdns-admin |
| sqla_user_loginhost | The host / network from which the db accepts connection |
| sqla_db_password | The password for the pdns-admin db user |
| sqla_db_name | The name of the database for pdns-admin |

### schema of pdns_admin__database_credentials

| Key | Comments (type) |
| --- | --- |
| priv_user | The database user that has permission to create the pdns-admin database and user |
| priv_password | The password to log the `priv_user` into the database server |
| priv_host | The IP-address / hostname of the database server |


Dependencies
------------

None.

Example Playbook
----------------

    - hosts: pdnsadmin_servers
      roles:
        - role: pdns_admin
          vars:
            pdns_admin__install_mode: docker
            pdns_admin__database_config:
              sqla_db_user: pdnsa
              sqla_db_password: SupaSicretPasswurt
              sqla_db_name: pdnsa
            pdns_admin__database_credentials:
              priv_user: root
              priv_host: mydb-server.lan
              priv_password: AnotherSecretPassword

License
-------

GPL v3

Author Information
------------------

Original implementation by Jascha Sticher (-1855)
