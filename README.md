# ansible-kvm-kickstart

Description
-----------

A set of Ansible roles, playbooks, and sample inventory files to build a KVM virtualization environment on RHEL/CentOS 7.  The environment will be configured to provide PXE and Kickstart functionality over an internal network bridge interface for unattended install of virtual systems.  Using templated libvirt XML configuration files, virtual machines can be defined,  provisioned, and installed quickly using Ansible playbooks with no interactivity required.

Usage
-----

With the provided playbooks, roles, and inventory files you should be able to configure a running RHEL/CentOS 7 system for KVM with some small changes to the host and group variables.

This playbook will configure the KVM environment.

    ansible-playbook 00_configure_kickstart_kvm.yml

This playbook will provision as many guest systems as are defined in the inventory.

    ansible-playbook 01_provision_guests.yml

host_vars and group_vars are used extensively to provide the specifications of each system being provisioned, so as to make the process completely self-guiding.  The example inventory files show all the information required to build a KVM virtualization environment on a server and create 3 guest systems.

Each role has detailed documentation explaining the specific requirements and variable definitions required for its use.

License
-------

MIT

Author Information
------------------

Christopher Costa, christopher.costa@gmail.com
