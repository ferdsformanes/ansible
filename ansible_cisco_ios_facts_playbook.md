# Ansible Cisco IOS Facts Playbook Guide

This example shows how to gather facts from a Cisco IOS device using the `cisco.ios.ios_facts` module and display the device hostname and IOS version.

## Prerequisites

- Ansible installed
- Cisco IOS collection installed:

```bash
ansible-galaxy collection install cisco.ios
```

- Save `inventory.yml` and `gather_cisco_facts.yml` in the same directory.
- Replace the example IP address and username with your actual device details.

---

## inventory.yml

> **Important:** Replace `192.168.1.10` with the actual device IP address and replace `your-username` with your actual username.

```yaml
all:
  children:
    cisco:
      hosts:
        192.168.1.10:
      vars:
        ansible_connection: network_cli
        ansible_network_os: cisco.ios.ios
        ansible_user: your-username
```

---

## gather_cisco_facts.yml

```yaml
---
- name: Gather Cisco Facts
  hosts: cisco
  gather_facts: false

  tasks:
    - name: Gather Cisco facts
      cisco.ios.ios_facts:

    - name: Display hostname and version
      debug:
        msg: "Hostname={{ ansible_net_hostname }} Version={{ ansible_net_version }}"
```

---

## Run the Playbook

```bash
ansible-playbook -i inventory.yml gather_cisco_facts.yml -k
```

---

## Example Output

```text
TASK [Display hostname and version] *******************************************

ok: [192.168.1.10] => {
    "msg": "Hostname=SW1 Version=17.09.04a"
}
```

---

## Notes

- `cisco.ios.ios_facts` collects information from the Cisco device.
- `ansible_net_hostname` contains the device hostname.
- `ansible_net_version` contains the Cisco IOS software version.
- `-k` prompts for the SSH password.
- The inventory group name `cisco` matches the `hosts: cisco` entry in the playbook.
