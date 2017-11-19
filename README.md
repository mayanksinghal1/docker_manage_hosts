docker_call_api
=========

This role is a collections of plays that call the Docker api.

Requirements
------------

The Control Node must have Docker installed.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

None.
Example Playbook
----------------

The `main.yml` file tests the plays and is called as follows:

    - hosts: servers
      roles:
         - { role: docker_call_api }

License
-------

Apache

Author Information
------------------

Ian Turner
Snr DevOps Technician
Atos SE
