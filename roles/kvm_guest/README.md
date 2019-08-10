Role Name
=========

An Ansible Role to configure a guest server on a KVM hypervisor using libvirt XML templates.

Requirements
------------

* Ansible 2.5. Backward compatibility with older versions of Ansible is not guaranteed.
* A target system running RHEL/CentOS 7 with access to the default yum repositories.
* One or more members of the 'kvm-servers' inventory group.  One of which will be the hypervisor for the guest systems.
* One or more members of the 'pxe-clients' inventory group.  Each of which will get provisioned on the hypervisor.

Role Variables
--------------

The XML templates require specific details about the amount of memory, processors, and storage for each guest system.   Some reasonable default values are provided to build a small system.

    vm_memory: 1536
    vm_memory_unit: MiB
    vm_cpus: 1
    vm_disk_size: 30G

The role needs a variable containing the inventory hostname of the KVM host (hypervisor) on which to provision the systems.   By default, the role chooses the first host in the 'kvm-servers' inventory group.

    hypervisor: "{{ groups['kvm-servers'][0] }}"

Each guest system can define a 'vm_xml_template' with specific details about the VM to create.  A default template is provide, and the role will use that template by default.  Custom templates can be placed in the role templates directory.

    vm_xml_template: default.xml.j2

Within the templates, some information about the guest and the host is required.  For the guest, the MAC address of both the public and PXE boot interfaces need to be defined.  There are no defaults for these variable, and they must be explicitly defined and passed to the role or set outside the role.

    pxe_mac
    sys_mac

Also, the name of the public interface of the host is required.  This is used to specify where to bind the public interface of the guest, so it can be bridged to the external network.  This must be defined as a hostvar for the KVM server.

    sys_int

Variable are used to control whether a VM is started and/or configured to autostart after being created.  It might not be optimal to boot every system at the same time, depending on how powerful the KVM server is and the number of guests being created at once.  By default, hosts will start automatically after provisioning but will not be configured to autostart when the KVM server comes online.

    vm_start: True
    vm_autostart: False

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: pxe-clients
      roles:
         - role: kvm_guest
           args:
             vm_autostart: True
             vm_cpus: 2
             vm_disk_size: 100G

License
-------

MIT

Author Information
------------------

Christopher Costa, christopher.costa@gmail.com
