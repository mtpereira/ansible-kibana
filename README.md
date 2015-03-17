Kibana [![Build Status](https://travis-ci.org/mtpereira/ansible-kibana.svg)](https://travis-ci.org/mtpereira/ansible-kibana)
=========

Ansible role for Kibana 4.

It installs Kibana from the tarballs available at [Kibana's official page](https://www.elastic.co/downloads/kibana) by default. The init script was generated using [Pleaserun](https://github.com/jordansissel/pleaserun).

It has been developed on Ubuntu 14.04 (Trusty) but it should work on other Debian systems.

Requirements
------------

None.

Role Variables
--------------

Required variables:

* `kibana_tarball`: Name of the tarball to fetch from `kibana_url`. Defaults to `kibana-4.0.1-linux-x64.tar.gz`.
* `kibana_tarball_checksum`: SHA256 sum of the tarball. It's used to check the validity of the tarball.
* `kibana_url`: URL from where the tarball will be fetched. Defaults to `https://download.elasticsearch.org/kibana/kibana`.
* `kibana_install_dir`: Base path for installation. Defaults to `/opt`.
* `kibana_user`: User that will run Kibana. Defaults to `kibana`.
* `kibana_group`: Group for the `kibana_user`. Defaults to `kibana`.
* `kibana_port`: Bind port for Kibana. Defaults to `5601`.
* `kibana_bind`: Bind address for Kibana. Defaults to `127.0.0.1`.
* `kibana_elasticsearch_url`: Elasticsearch URL where Kibana will connect. Defaults to `http://localhost:9200`.
* `kibana_request_timeout`: Time in milliseconds to wait for responses from Elasticsearch. Must be greater than 0. Defaults to `300000`.
* `kibana_default_app`: The default view for Kibana, e.g., "discover", "visualize", "dashboard". Defaults to "discover".
* `kibana_shard_timeout`: Time in milliseconds for Elasticsearch to wait for responses from shards. Set to `0` to disable. Defaults to `0`.
* `kibana_verify_ssl`: Set to false to have a complete disregard for the validity of the SSL. Defaults to `true`.
* `kibana_pid`: Path for Kibana's PID file, managed by the init script and not by Kibana. The `pid_file` configuration of Kibana is not changed, since it would conflict with our init script and require mangling with `/var/run` directory permissions. Defaults to `/var/run/kibana.pid`.
* `kibana_running`: Start service after installation and configuration. Defaults to `true`.

Local facts:

This role installs some local facts for guaranteeing idempotency and also for easier integration with other roles.

* `ansible_local.kibana.url`: URL from where the currently installed Kibana was fetched from.
* `ansible_local.kibana.tarball`: Tarball used for the currntly installed Kibana.
* `ansible_local.kibana.tarball_checksum`: Tarball's checksum used of the currently installed Kibana.
* `ansible_local.kibana.install_dir`: Base path where Kibana is installed.
* `ansible_local.kibana.port`: Bind port of the current configuration.
* `ansible_local.kibana.bind`: Bind address of the current configuration.

Internal variables, avoid changing:

* `kibana_download_dir`: Directory where the tarball will be downloaded to. Defaults to `/tmp`.
* `kibana_tarball_name`: Basename of the `kibana_tarball` file. Used for getting the extracted dir name. Defaults to `"{{ kibana_tarball | replace('.tar.gz', '') }}"`.

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: mtpereira.kibana }

License
-------

BSD

Author Information
------------------

[GitHub project page](https://github.com/mtpereira/ansible-kibana)

[Manuel Tiago Pereira](http://mtpereira.github.io)

