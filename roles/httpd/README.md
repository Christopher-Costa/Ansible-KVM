Ansible Role: httpd
=========

An Ansible Role to install, configure, enable, and start an Apache httpd service for serving Kickstart files and network operating system installations.

Requirements
------------

* Ansible 2.5. Backward compatibility with older versions of Ansible is not guaranteed.
* A target system running RHEL/CentOS 7 with access to the default yum repositories.
* A copy of a RHEL/CentOS 7 ISO image available on the target system.  The accompanying "kvm" role copies a .iso file intended for this purpose, but that isn't a strict requirement.
* Guests will be expected to have at least two network interfaces.  One for attaching to a local bridge for handling the internal PXE Boot / Kickstart services, and a second for standard network connectivity. 
* Guests must belong to an inventory group named 'pxe_clients' in order for a kickstart template to be generated and installed.

Role Variables
--------------

The role requires a location for an ISO image to be defined, which will be extracted to create a network installation repository.   The location defaults to the path where the accompanying "kvm" role installs its ISO file.

    iso_path: /var/lib/libvirt/images

Kickstart templates can be configured in hostvars, otherwise a default template will used.  Custom templates should be placed in *templates/var/www/html/ks/*

    default_kickstart_template: default.ks.j2

Since this role will install templated Kickstart files for guests, certain variables must be defined as hostvars for each system and have no defaults.

    pxe_int:    eth0
    pxe_ip:     192.168.255.10
    sys_int:    eth1
    sys_ip:     10.0.0.10
    kickstart_template: custom.ks.j2

Some additional variables are required for templated Kickstart, but can be be defined outside of the host context since they are more broadly scoped.

    pxe_netmask: 255.255.255.0
    sys_netmask: 255.255.255.0
    sys_dns: 8.8.8.8,8.8.4.4
    sys_gateway: 10.0.0.1

Other variables are defined for whether or not to start and/or enable the httpd service after installation.  By default, the service is both started and enabled.

    enable_httpd_service: True
    start_httpd_service: True

Dependencies
------------

The role expects either the accompanying "kvm" role, or for an ISO installation image to have been copied to the target system.

Example Playbook
----------------

    - hosts: kvm_servers
      roles:
         - role: httpd
           vars:
             iso_path: my/image.iso

License
-------

MIT

Author Information
------------------

Christopher Costa, christopher.costa@gmail.com
