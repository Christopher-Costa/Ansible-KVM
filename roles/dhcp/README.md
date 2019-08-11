Ansible Role: dhcp
=========

An Ansible Role to install, configure, enable, and start the dhcpd service on a RHEL/CentOS 7 system, and configure it to assign static network information to a defined list of clients to support a PXE Boot/Kickstart service.

Requirements
------------

* Ansible 2.5. Backward compatibility with older versions of Ansible is not guaranteed.
* A target system running RHEL/CentOS 7 with access to the default yum repositories.
* Proper variable or group/hostvars declarations for DHCP clients with required information (see below).
* A network interface with an IPv4 address to serve DHCP over.  The accompanying "bridge_interface" role is intended to facilitate this, but isn't a strict requirement.

Role Variables
--------------

The role requires a list of systems which are to be DHCP clients, along with the IP Address and MAC Address to be assigned to each client by the DHCP server.  This information is used to create the dhcpd.conf configuration file, and can be provided in one or both of two different ways.

1.  A *variable* named *pxe_clients*, which is a list of clients including nested variables for pxe_ip and pxe_mac.  This variable defaults to an empty list in defaults/main.yml, and must be explicitly defined and passed to the role or set externally if it is to be used. 

        pxe_clients: [] 

2. A *group* named *pxe_clients* containing inventory hosts, with associated hostvars defined for pxe_ip and pxe_mac. The role expects there to be hostvars containing the IP address and MAC address to be assigned by the server. 

        pxe_ip:     192.168.255.02
        pxe_mac:    00:00:01:00:00:02

The role also requires a variable named pxe_int containing the name of the interface serving DHCP.   There is no default for this variable, and it must be explicitly defined and passed to the role or set outside the role. Ansible will gather facts on the target system and use this interface name to reference the IP, network, and broadcast addresses, along with the subnet mask of the interface for use in the dhcpd.conf configuration file.

Other variables are defined for whether or not to start and/or enable the dhcpd service after installation.  By default, the service is both started and enabled.

    enable_dhcpd_service: True
    start_dhcpd_service: True

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: kvm_servers
      roles:
        - role: dhcp
          vars:
            pxe_int: brpxe0
            pxe_clients:
              client1:
                pxe_ip: 10.0.0.1
                pxe_mac: 00:00:01:00:00:01
              client2:
                pxe_ip: 10.0.0.2
                pxe_mac: 00:00:01:00:00:02

License
-------

MIT

Author Information
------------------

Christopher Costa, christopher.costa@gmail.com
