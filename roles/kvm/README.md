Ansible Role: kvm
=========

An Ansible Role to install, enable, and start KVM hypervisor on a system running a minimal install of RHEL/CentOS 7.  An ISO image will be copied, to be used to provision guests.

Requirements
------------

* Ansible 2.5. Backward compatibility with older versions of Ansible is not guaranteed.
* A target system running RHEL/CentOS 7 with access to the default yum repositories.
* A locally accessible RHEL/CentOS 7 ISO image to be uploaded to the target system.

Role Variables
--------------

The role has several variables defined in defaults/main.yml.  The first is the list of packages to be installed for a basic KVM hypervisor.

    kvm_packages:
      - qemu-kvm
      - qemu-img
      - virt-manager
      - libvirt
      - libvirt-python
      - libvirt-client
      - virt-install
      - virt-viewer

The role defines default values for the local and remote path for the .iso file.  By default the role expects the .iso file to be found in a directory named 'files' within the playbook directory.  By default the role will copy the file to the standard KVM image store.  By default the .iso file will be owned by the root user but be world readable.  The name of the .iso file is provided in a variable called 'iso_name' and has no default value.  It must be explicitly defined and passed to the role or set outside the role.

    local_iso_path: "{{ playbook_dir }}/files"
    iso_path: /var/lib/libvirt/images
    iso_owner: root
    iso_group: root
    iso_mode: 0644

Other variables are defined for whether or not to start and/or enable the libvirtd service after installation.  By default, the service is both started and enabled.

    start_kvm_service: True
    enable_kvm_service: True

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: kvm_servers
      roles:
        - role: kvm
          vars:
            start_kvm_service: False
            iso_name: my_CentOS_image.iso

License
-------

MIT

Author Information
------------------

Christopher Costa, christopher.costa@gmail.com
