ossec-agent
=========
Used for install and automatic key generation of OSSEC clients.  Will

- Connects to the OSSEC server and uses a batch control script to generate keys.
- Uses the keys grabbed from the script to register the hosts.

Requirements
------------
Ansible needs control of the ossec server to install the file to manage batch clients.

Role Variables
--------------
Please define the following variables in host_vars for your server.

WINDOWS HOST VARS:
 - ossec_url:
   - URL to obtain the OSSEC windows package to install
 - ossec_file:
   - Name of the file used in package above.
 - ossec_server:
   - The IP address of your OSSEC server.

LINUX HOST VARS:
 - ip_address
   - The IP address to use to register your host.  You can use ansible defined variable or type it in.
 - ossec_server
   - The OSSEC server your client will make connections to.

Example host_vars file:
```sh
#Windows hosts vars to define
ossec_url: 'https://updates.atomicorp.com/channels/atomic/windows/ossec-agent-win32-2.9.0-1738.exe'
ossec_file: 'ossec-agent-win32-2.9.0-1738.exe'
ossec_server: 'X.X.X.X'

#Linux host vars to define
ip_address: "{{ ansible_all_ipv4_addresses.0 }}"
ossec_server: 'X.X.X.X'
```

Dependencies
------------
- Function OSSEC server running Linux

Example Playbook
----------------

```sh
- name: OSSEC agent install.
  hosts: xx-xx-server
  roles:
     - bouncingsoles.ossec-agent
  become: yes
```

License
-------
BSD

Author Information
------------------
Patrick Durante
