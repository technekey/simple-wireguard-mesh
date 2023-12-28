# simple-wireguard-mesh
## Overview
This Ansible playbook automates the creation of a WireGuard mesh network on Ubuntu 22.04 virtual machines. The goal is to simplify the setup process, requiring minimal configuration and no underlying knowledge of WireGuard. The playbook is designed for ease of use and can be considered a "shoot and forget" solution for setting up a basic WireGuard mesh.

## Features
Automated WireGuard Mesh: The playbook automates the creation of a WireGuard mesh network among the specified hosts in your inventory file.

## Minimal Configuration: 
No advanced knowledge of WireGuard is required. The playbook is designed to work with a properly set up inventory file.

## Tested Environment: 
The playbook has been tested on Ubuntu 22.04 virtual machines. While it should work on other distributions, it is specifically tailored for Ubuntu 22.04.

## Scalability: 
Plans include support for dynamically adding and removing nodes from the WireGuard mesh, providing flexibility for changing network configurations.

## Prerequisites
- Ansible: Ensure that Ansible is installed on your control machine.
- Bunch of Target VMs

### Usage
- Configure Your Inventory File: Update your Ansible inventory file with the details of your Ubuntu 22.04 virtual machines.
- You can update the configuration parms inside groupvars directory if needed. This is optional. ( you will find a lot of explanatory comments)

- Run the Playbook: Execute the Ansible playbook to create the WireGuard mesh network.

```
ansible-playbook -i inventory.yml main.yml
```
In case you want to overwrite the existing wireguard config, you will have to use `-e overwrite=yes` extra vars. 
Sit Back and Relax: The playbook will automate the WireGuard mesh setup. No further actions are needed.


### Example:
With the following Virtual machine as target, a mesh will be created.
```
192.168.122.116 wg1
192.168.122.99 wg2
192.168.122.238 wg3
```

Here are the config files generated on the three machines:

```
wg1

#vm1(Self)
[Interface]
PrivateKey = sKDaZuQGOQHvkLZ/1WEypshoX78rySJtWvQwLxn7Q14=
Address = 10.0.0.2
ListenPort = 51819

PostUp = iptables -A FORWARD -i %i -j ACCEPT; iptables -t nat -A POSTROUTING -o enp1s0 -j MASQUERADE
PostDown = iptables -D FORWARD -i %i -j ACCEPT; iptables -t nat -D POSTROUTING -o enp1s0 -j MASQUERADE

#vm2
[Peer]
PublicKey = WbZwBrC3FEo4F+saB6k6w3fbJB7MD7bk+8wsuNFd9zI=
Endpoint = 192.168.122.99:51819
AllowedIPs = 10.0.0.3/32
PresharedKey = XUhu0hl1FwXr5WorcMIf2hYzPm+fWtsFRgrBVCVzBG4=
PersistentKeepalive = 30
#vm3
[Peer]
PublicKey = Tr1ivpcVtoAuPhYlG+p6Qqo/s9mNlLYYmIlqAol4yQI=
Endpoint = 192.168.122.238:51819
AllowedIPs = 10.0.0.4/32
PresharedKey = XUhu0hl1FwXr5WorcMIf2hYzPm+fWtsFRgrBVCVzBG4=
PersistentKeepalive = 30





wg2

#vm2(Self)
[Interface]
PrivateKey = +ERl8D/3gc24iG6BUgqG1GwgJMQbf37LQpoEUhPkZGM=
Address = 10.0.0.3
ListenPort = 51819

#vm1
[Peer]
PublicKey = T+2g5kScp3YqLj/9/RR/zsNnFT2/aqRtidYYbM8I40Q=
Endpoint = 192.168.122.116:51819
AllowedIPs = 10.0.0.2/32
PresharedKey = XUhu0hl1FwXr5WorcMIf2hYzPm+fWtsFRgrBVCVzBG4=
PersistentKeepalive = 30
#vm3
[Peer]
PublicKey = Tr1ivpcVtoAuPhYlG+p6Qqo/s9mNlLYYmIlqAol4yQI=
Endpoint = 192.168.122.238:51819
AllowedIPs = 10.0.0.4/32
PresharedKey = XUhu0hl1FwXr5WorcMIf2hYzPm+fWtsFRgrBVCVzBG4=
PersistentKeepalive = 30




wg3

#vm3(Self)
[Interface]
PrivateKey = GHMhzwX/tAqfUgND32+Zxv5S8dV8k9oIkA9GMVqFFlU=
Address = 10.0.0.4
ListenPort = 51819

#vm1
[Peer]
PublicKey = T+2g5kScp3YqLj/9/RR/zsNnFT2/aqRtidYYbM8I40Q=
Endpoint = 192.168.122.116:51819
AllowedIPs = 10.0.0.2/32
PresharedKey = XUhu0hl1FwXr5WorcMIf2hYzPm+fWtsFRgrBVCVzBG4=
PersistentKeepalive = 30
#vm2
[Peer]
PublicKey = WbZwBrC3FEo4F+saB6k6w3fbJB7MD7bk+8wsuNFd9zI=
Endpoint = 192.168.122.99:51819
AllowedIPs = 10.0.0.3/32
PresharedKey = XUhu0hl1FwXr5WorcMIf2hYzPm+fWtsFRgrBVCVzBG4=
PersistentKeepalive = 30

```

### Important Notes
#### Distribution Compatibility:
While the playbook is tailored for Ubuntu 22.04, it may work on other distributions. However, it's recommended to test in your specific environment.

#### Not Production-Grade:
This playbook is designed for personal use and may not meet the security and scalability requirements of a production environment. Use it in a controlled setting.

### Contribution
Contributions and improvements are welcome! If you encounter issues or have ideas for enhancements, feel free to open an issue or submit a pull request.
### License
This project is licensed under the MIT License.
