Ansible Role: xrdp
=========

An Ansible Role to install, configure, enable, and start the xRDP application for remote desktop access.

Requirements
------------

* Ansible 2.5. Backward compatibility with older versions of Ansible is not guaranteed.
* A target system running RHEL/CentOS 7 with access to the default yum repositories.
* The target system must run firewalld.

Role Variables
--------------

The role has several variables defined in defaults/main.yml.  The first is the list of xRDP packages to be installed.

    xrdp_packages:
      - xrdp
      - tigervnc-server

The role allows for configuration of a custom port for xRDP.   The role uses the standard 3389 port as the default.  When customized, the xrdp and firewalld configurations will be set appropriately.

    xrdp_port: 3389

Other variables are defined for whether or not to start and/or enable xrdp after installation.  By default, the service is both started and enabled.

    start_xrdp_service: True
    enable_xrdp_service: True

The role provides a variable for specificing the firewalld zone on which to apply the rule.   This defaults to the "public" zone.

    xrdp_firewalld_zone: public 

Dependencies
------------

xrdp is available through the EPEL repositories, so the 'epel-release' package must be installed as a dependency. 

Example Playbook
----------------

    - hosts: kvm-servers
      roles:
         - role: xrdp

License
-------

MIT

Author Information
------------------

Christopher Costa, christopher.costa@gmail.com
