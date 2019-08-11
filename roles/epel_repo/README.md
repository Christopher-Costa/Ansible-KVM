Ansible Role: epel_repo
=========

An Ansible Role to install the EPEL repositories on a RHEL/CentOS 7 system.

Requirements
------------

* Ansible 2.5. Backward compatibility with older versions of Ansible is not guaranteed.
* A target system running RHEL/CentOS 7 with access to the default yum repositories.

Role Variables
--------------

None.

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: kvm_servers
      roles:
        - role: epel_repo

License
-------

MIT

Author Information
------------------

Christopher Costa, christopher.costa@gmail.com
