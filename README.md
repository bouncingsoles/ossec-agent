ossec-agent
=========
Used for install and automatic key generation of OSSEC clients.  This role allows you to register hosts on Windows and Linux without having to enable auto-enroll or install any additional services.  

- Connects to the OSSEC server and uses a batch control script (included) to generate keys.
- Uses the keys generated in the playbook to register the hosts for Windows and Linux.

Requirements
------------
On the host you run the playbook, Ansible needs to be able to access your Ossec server to install the file to manage batch clients.
See project: https://github.com/ossec/ossec-hids/blob/master/contrib/ossec-batch-manager.pl

Role Variables
--------------
Please define the following variables in host_vars for your server.

WINDOWS HOST VARS:
 - ip_address
   - The IP address to use to register your host.  You can use ansible defined variable or type it in.
 - ossec_url:
   - URL to obtain the OSSEC windows package to install
 - ossec_file:
   - Name of the file used in package above.
 - ossec_server:
   - The IP address of your OSSEC server, this will be added to the ossec conf template file.

LINUX HOST VARS:
 - ip_address
   - The IP address to use to register your host.  You can use ansible defined variable or type it in.
 - ossec_server
   - The IP address of your OSSEC server, this will be added to the ossec conf template file.

EXTRA_VARS:
 - ossec_server_name: 
   - Hostname of you ossec server.  You can add this to the playbook like in the example below as vars.

Example host_vars file:
```sh
#Windows hosts vars to define
ip_address: "{{ ansible_ip_addresses.0 }}"
ossec_url: 'https://updates.atomicorp.com/channels/atomic/windows/ossec-agent-win32-2.9.0-1738.exe'
ossec_file: 'ossec-agent-win32-2.9.0-1738.exe'
ossec_server: 'X.X.X.X'

#Linux host vars to define
ip_address: "{{ ansible_all_ipv4_addresses.0 }}"
ossec_server: 'X.X.X.X'
```

Dependencies
------------
- A working OSSEC server running Linux that can be controlled by your host running Ansible.

Example Playbook
----------------

```sh
- name: OSSEC agent install.
  hosts: xx-xx-server
  roles:
     - bouncingsoles.ossec-agent
  vars:
  #Your OSSEC server, tasks to create keys will be delegate_to it.
    ossec_server_name: ossec-servername-01

```

License
-------
BSD

Author Information
------------------
Patrick Durante
