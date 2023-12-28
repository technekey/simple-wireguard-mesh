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

- Run the Playbook: Execute the Ansible playbook to create the WireGuard mesh network.

```
ansible-playbook -i inventory.yml main.yml
```
Sit Back and Relax: The playbook will automate the WireGuard mesh setup. No further actions are needed.

### Important Notes
#### Distribution Compatibility:
While the playbook is tailored for Ubuntu 22.04, it may work on other distributions. However, it's recommended to test in your specific environment.

#### Not Production-Grade:
This playbook is designed for personal use and may not meet the security and scalability requirements of a production environment. Use it in a controlled setting.

### Contribution
Contributions and improvements are welcome! If you encounter issues or have ideas for enhancements, feel free to open an issue or submit a pull request.
### License
This project is licensed under the MIT License.
