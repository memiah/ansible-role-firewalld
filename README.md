Firewalld
==================

Configure services and ports in firewalld.

Requirements
------------

Firewalld installed on target machine.

Role Variables
--------------

Available variables are listed below, along with default values (see 
`defaults/main.yml`):

    firewalld_enabled: True

By default, the firewalld configuration is enabled, so skip set to `False`. 

    firewalld_reload: True

Trigger a reload of the firewalld service, after configuring the specified configuration options.

    __firewalld_services:
      ssh:
        permanant: true
        state: enabled

By default, ensure the ssh service is enabled.

    firewalld_services: {}

Additional services to enable, these are merged with `__firewalld_services`. 
For a list of available services, run the `firewall-cmd --get-service` command on the provisioned server.

    firewalld_ports: {}

Ports and protocols to configure.

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: servers
      become: yes
      vars_files:
        - vars/main.yml
      roles:
        - memiah.firewalld

*Inside `vars/main.yml`*:

    firewalld_services:
      http:
        zone: public
        state: enabled
        permanant: true
      https:
        state: enabled
        
     firewalld_ports:
       mysql:
         port: 3306
         protocol: tcp
         state: enabled
         zone: public
         permanent: true

License
-------

MIT / BSD

Author Information
------------------

This role was created in 2016 by [Memiah Limited](https://github.com/memiah).
