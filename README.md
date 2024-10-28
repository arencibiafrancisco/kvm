# KVM Playbook Instructions

This document provides guidance on how to apply the `kvm-playbook.yml` playbook against the hypervisors using Ansible and how to understand the associated `hosts.ini` inventory file.

## `hosts.ini` Inventory File Explanation

The `hosts.ini` file is an Ansible inventory file that defines one group:

- `[hypervisors]`: This group should contain a list of hypervisor hosts. You'll need to list the IP addresses or hostnames of the hypervisors below this line.

Example:
```ini
[hypervisors]
172.18.1.10
172.18.1.20

```
## Applying the Playbook to Hypervisors

To run the playbook against the hypervisors, use the following command:

```bash
ansible-playbook -i hosts.ini kvm-playbook.yml -u root -e "cloudbr0_ip=10.35.2.23/24 cloudbr0_gw=10.5.2.1 dns_servers=8.8.8.8,1.1.1.1 cloudbr1_ip=10.35.5.61/24"
```

## Running Specific Roles
To execute selected roles only, use the --tags option:

For the KVM installation role:

```bash
ansible-playbook kvm-playbook.yml -i  hosts.ini -u root --tags "kvm"
```

For the Cockpit installation role:

```bash
ansible-playbook kvm-playbook.yml -i  hosts.ini -u root --tags "cockpit"
```

For network configuration:

```bash
ansible-playbook kvm-playbook.yml -i  hosts.ini -u root --tags "network" -e "cloudbr0_ip=10.35.2.23/24 cloudbr0_gw=10.5.2.1 dns_servers=8.8.8.8,1.1.1.1 cloudbr1_ip=10.35.5.61/24"
```

To run multiple roles (KVM and cockpit):

```bash
ansible-playbook kvm-playbook.yml -i  hosts.ini -u root --tags "kvm, cockpit"
```
