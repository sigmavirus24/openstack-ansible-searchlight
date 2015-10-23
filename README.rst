OpenStack Searchlight
=====================

A simple role to deploy OpenStack Searchlight from source in a manner similar 
to the OpenStack Ansible project.

Requirements
------------

None.

Role Variables
--------------

See ``defaults/main.yml`` for variables and their descriptions.

Dependencies
------------

None.

Example Playbook
----------------

.. code-block:: yaml

    - hosts: servers
      roles:
         - { role: sigmavirus24.openstack-ansible-searchlight }

License
-------

Apache

Credits
-------

The ``config_template`` library module was developed by Kevin Carter for the
OpenStack Ansible and is vendored in ``library``.
