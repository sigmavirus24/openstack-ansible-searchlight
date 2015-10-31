==============================================
 Using the openstack-ansible-searchlight role
==============================================

Below is some very high-level documentation for using this role.

Install Role
============

Create a file called ``requirements.yml`` with the contents:

.. code-block:: yaml

    - name: elasticsearch
      src: Stouts.elasticsearch

    - name: searchlight
      src: https://github.com/sigmavirus24/openstack-ansible-searchlight

To install the role then do:

.. code::

    $ ansible-galaxy install -r requirements.yml

Using the role with OpenStack Ansible
=====================================

An example playbook might look like:

.. code-block:: yaml

    # os-searchlight-install.yml
    ---
    - hosts: elasticsearch_all
      roles:
      - role: Stouts.elasticsearch
      
    - hosts: searchlight_all
      roles:
      - role: pip_lock_down
      - role: sigmavirus24.openstack-ansible-searchlight

If you're using this role with the OpenStack Ansible, you'll want to add a 
line to your ``/etc/openstack_deploy/user_secrets.yml`` and rerun the password 
generation script:

.. code-block:: yaml

    searchlight_service_password:

You will need to make a file named ``searchlight.yml`` in 
``/etc/openstack_deploy/env.d/`` with the following contents:

.. code-block:: yaml

    # /etc/openstack_deploy/env.d/searchlight.yml
    ---
    component_skel:
      searchlight_api:
        belongs_to:
          - searchlight_all

    container_skel:
      searchlight_container:
        belongs_to:
          - infra_containers
          - os-infra_containers
        contains:
          - searchlight_api
        properties:
          service_name: searchlight
          contianer_release: trusty

Note that under properties you can also specify whether searchlight runs in a 
container or on bare metal with ``is_metal:`` set to ``true`` or ``false``.

You will also need to make a group for ``elasticsearch_all``.

Finally, just run the playbook above and you should have a functional 
Searchlight service.
