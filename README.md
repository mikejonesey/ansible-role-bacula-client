Role Name
=========

Install and add basic configuration for the bacula-fd agent. The role supports Debian, Ubuntu and CentOS.

Requirements
------------

1. passwordstore (sudo apt-get install pass), https://docs.ansible.com/ansible/latest/collections/community/general/passwordstore_lookup.html
passwords for fd agents are stored locally in pass db (gpg encrypted).

2. A bacula server, this role is for the agent only, not the server. The role will whitelist the server defined using var "bacula_server_address"

Role Variables
--------------

All variables used are defined in the defaults file, which can be overriden in either host_var or group_var;

All variables specific to this roll are prepended with "bacula_client_"

#### Must overide variables ####

    none

#### Optional to overide variables ####

The Agent Name (defaults auto-generated)

    bacula_client_name: "fd-{{ ansible_hostname }}"
    
Bacula Dir name defined in bacula server, this is the same across all of your agents.

    bacula_server_dir: "dir-name"
    
switch from OS packages to bacula systems comminity packages, define the community version and key 
    
    bacula_community_binaries: yes
    bacula_community_version: "9.4.2"
    bacula_community_key: "xxxxxxxxxxxxx"


Dependencies
------------

The following roles can be run prior to installing agents, or use other roles for these tasks...

roles:
 - bacula = setup and configure a bacula server (not required to run this role, but useless without).

optional roles:
 - local-password-store = setup and configure "pass" tool locally for use with ansible to store passwords.

Example Playbook
----------------

Play can target any host in inventory.

    - hosts: all
      become: yes
      roles:
        - bacula-client
      tags: bacula,backup


License
-------

BSD

Author Information
------------------

Michael Jones <mj@mikejonesey.co.uk>
