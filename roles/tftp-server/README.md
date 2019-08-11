Ansible Role: tftp-server
=========

An Ansible Role to install, configure, enable, and start a TFTP service for PXE Boot.

Requirements
------------

* Ansible 2.5. Backward compatibility with older versions of Ansible is not guaranteed.
* A target system running RHEL/CentOS 7
* Guests must belong to an inventory group named 'pxe_clients' in order for a pxelinux.cfg file to be generated and installed on the TFTP server.

Role Variables
--------------

Since this role will install templated pxelinux.cfg files for guests, the variable 'pxe_ip' must be definted in hostvars for each system.   That variable will not have a default value.

    pxe_ip: 192.168.255.10

The role also requires a variable named 'pxe_ip' containing the IP address of the PXE Boot interface.  There is no default for this variable, and it must be explicitly defined and passed to the role or set outside the role.

    pxe_ip: 192.168.255.1

Variables are defined for whether or not to start and/or enable the tftp service after installation. By default, the service is both started and enabled.

    enable_tftp_service: True
    start_tftp_service: True

Dependencies
------------

The 'syslinux' package must be installed as a dependency.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: kvm-servers
      roles:
         - role: tftp-server
           vars:
             pxe_ip: 192.168.0.1

License
-------

MIT

Author Information
------------------

Christopher Costa, christopher.costa@gmail.com
