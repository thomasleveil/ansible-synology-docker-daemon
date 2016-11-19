Synology Docker daemon
======================

This Ansible role manages the Docker daemon options.

By default, the Synology Docker daemon is started with just the `--ipv6=true` option, I needed to set custom DNS options.

[![Travis CI](https://img.shields.io/travis/thomasleveil/ansible-synology-docker-daemon.svg?style=flat)](https://travis-ci.org/thomasleveil/ansible-synology-docker-daemon)
[![Platforms](http://img.shields.io/badge/platforms-Synology 6.0-lightgrey.svg?style=flat)](#)

Requirements
------------

This role was tested with Ansible 2.2. It probably works with 2.0 and 2.1 (let me know).

Tested with Synology `DSM 6.0.2-8451 Update 3` which comes with `Docker 1.11.2`.

Any change to the DSM version or Docker version might break this role.


Role variables
--------------

There is only one variable: `docker_opts` which is a list of options.

    docker_opts:
     - --dns 8.8.8.8
     - --dns 8.8.4.4
     - --ipv6=true


Examples
--------

    - hosts: all
      roles:
       - ansible-synology-docker-daemon
      vars:
        docker_opts:
          - --dns 8.8.8.8
          - --dns 8.8.4.4
          - --dns 208.67.222.222
          - --ipv6=true

----

How to add this role to your git repository with submodules
-----------------------------------------------------------

    # new ansible project
    mkdir ansible-nas
    cd ansible-nas
    
    # initialize git
    git init
    
    # Add the role
    git submodule add https://github.com/thomasleveil/ansible-synology-docker-daemon.git roles/ansible-synology-docker-daemon
    
    # Create a playbook
    cat <<EOPLAY > synology.yml
    - hosts: all
      roles:
       - ansible-synology-docker-daemon
      vars:
        docker_opts:
          - --dns 8.8.8.8
          - --dns 8.8.4.4
          - --dns 208.67.222.222
          - --ipv6=true
    EOPLAY
    
    git add .gitmodules roles/ansible-synology-docker-daemon/ synology.yml
    git commit -m "ansible-synology-docker-daemon role"
    
    # hack hack hack


