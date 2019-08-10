Ansible Role: syslinux
=========

An Asnible Role to install the syslinux package on a RHEL/CentOS 7 system.

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

    - hosts: kvm-servers
      roles:
         - role: syslinux

License
-------

MIT

Author Information
------------------

Christopher Costa, christopher.costa@gmail.com
