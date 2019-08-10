Ansible Role: pxe_bridge
=========

An Ansible Role to install and enable a network bridge interface to support a PXE Boot/Kickstart service.

Requirements
------------

* Ansible 2.5. Backward compatibility with older versions of Ansible is not guaranteed.
* A target system running RHEL/CentOS 7
* The target system must run firewalld.

Role Variables
--------------

The role requires three variables be set, which have no default values assigned.  These variables provide configuration details for the bridge interface.  They must be passed to the role or otherwise be declared outside of it.

    pxe_int:
    pxe_ip:
    pxe_netmask:

Another variable, 'pxe_server_zone', is used to define the FirewallD zone to place the bridge interface into.  Since an internal bridge interface isn't exposed to the outside world, it will be placed in the 'trusted' zone by default, in order to avoid PXE Boot/Kickstart traffic being blocked.

    pxe_server_zone: trusted

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: kvm-servers
      roles:
        - role: pxe_bridge
          vars:
            pxe_int: brtest0
            pxe_ip: 10.0.0.1
            pxe_netmask: 255.255.255.0

License
-------

MIT

Author Information
------------------

Christopher Costa, christopher.costa@gmail.com
