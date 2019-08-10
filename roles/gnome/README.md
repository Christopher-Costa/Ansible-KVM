Ansible Role: gnome
=========

An Ansible Role to install a very minimal GNOME desktop enviroment on a system running a minimal install of RHEL/CentOS 7.

Requirements
------------

* Ansible 2.5. Backward compatibility with older versions of Ansible is not guaranteed.
* A target system running RHEL/CentOS 7 with access to the default yum repositories.

Role Variables
--------------

The role has a variable defined in defaults/main.yml listing the packages to be installed for a minimal GNOME environment.

    gnome_packages:
      - "@X-Window-System"
      - gnome-classic-session
      - gnome-terminal
      - gnome-terminal-nautilus
      - control-center
      - liberation-mono-fonts
      - terminus-fonts

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: kvm-servers
      roles:
        - role: gnome

License
-------

MIT

Author Information
------------------

Christopher Costa, christopher.costa@gmail.com
