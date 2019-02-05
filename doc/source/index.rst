==============================
OpenStack-Ansible mistral role
==============================

This role installs the following Systemd services:

    * mistral-api
    * mistral-engine
    * mistral-executor
    * mistral-notifier

To clone or view the source code for this repository, visit the role repository
for `os_mistral <https://github.com/openstack/openstack-ansible-os_mistral>`_.

Default variables
~~~~~~~~~~~~~~~~~

.. literalinclude:: ../../defaults/main.yml
   :language: yaml
   :start-after: under the License.

Example playbook
~~~~~~~~~~~~~~~~

.. literalinclude:: ../../examples/playbook.yml
   :language: yaml

External Restart Hooks
~~~~~~~~~~~~~~~~~~~~~~

When the role performs a restart of the service, it will notify an Ansible
handler named ``Manage LB``, which is a noop within this role. In the
playbook, other roles may be loaded before and after this role which will
implement Ansible handler listeners for ``Manage LB``, allowing external roles
to manage the load balancer endpoints responsible for sending traffic to the
servers being restarted by marking them in maintenance or active mode,
draining sessions, etc. For an example implementation, please reference the
`ansible-haproxy-endpoints role <https://github.com/Logan2211/ansible-haproxy-endpoints>`_
used by the openstack-ansible project.

Tags
~~~~

This role supports two tags: ``mistral-install`` and ``mistral-config``.
The ``mistral-install`` tag can be used to install and upgrade. The
``mistral-config`` tag can be used to manage configuration.
