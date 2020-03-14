wireguard
=========

This role installs WireGuard, configures it as a server, sets up networking (iptables), and creates client configs with keys.

Tested OSes:
- Debian 10
- Ubuntu 18.04

Requirements
------------

Ansible >= 2.7 (It might work on previous versions, but we cannot guarantee it)

Role Variables
--------------

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) file.

Example Playbook
----------------

```yaml
- hosts: vpnserver
  roles:
    - role: wireguard
      become: yes
      wireguard_pub_address: "111.111.111.11"
      wireguard_network_name: vpn
      wireguard_external_net: "0.0.0.0/0"
      wireguard_dns_server: "208.67.222.222"
      wireguard_clients:
        - user_name: user1
          ip: "10.8.0.11"
        - user_name: user2
          ip: "10.8.0.12"
      wireguard_snat_ip: "{{ wireguard_pub_address }}"
```

Client confings
----------------
Client configs stored in "/etc/wireguard/clients" directory.
To change the client configs location, change "wireguard_clients_path" variable.
