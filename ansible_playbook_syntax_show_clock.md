# Ansible Playbook - Show Clock

This guide demonstrates how to convert an Ansible ad hoc command into a reusable playbook.

## Original Ad Hoc Command

```bash
ansible cisco -i inventory.yml -m cisco.ios.ios_command -a "commands='show clock'" -k
```

## Ansible Playbook Command Syntax

```bash
ansible-playbook -i <inventory> <playbook.yml> [options]
```

Example:

```bash
ansible-playbook -i inventory.yml show_clock.yml -k
```

Where:

- `<inventory>` - Inventory file containing the target hosts and connection variables.
- `<playbook.yml>` - The playbook file to execute.
- `[options]` - Optional parameters such as `-k`, `-u`, `-e`, and `-v`.

Unlike the `ansible` ad hoc command, `ansible-playbook` does not use a host pattern on the command line. The target hosts are defined inside the playbook using the `hosts:` parameter.

Example:

```yaml
- name: Show clock on Cisco devices
  hosts: cisco
```

In this example:

- `inventory.yml` tells Ansible where the hosts are located.
- `hosts: cisco` tells Ansible which hosts or group from the inventory should run the playbook.

## Inventory File

**inventory.yml**

```yaml
all:
  children:
    cisco:
      hosts:
        192.168.1.10:  # Replace with your Cisco device IP address
      vars:
        ansible_connection: network_cli
        ansible_network_os: cisco.ios.ios
        ansible_user: your_username  # Replace with your actual username
```

> **Note:**
>
> - Replace `192.168.1.10` with the actual IP address of your Cisco device.
> - Replace `your_username` with the username used to SSH into the device.
> - When running the playbook, Ansible will prompt for the password because the `-k` option is used.

## Playbook File

**show_clock.yml**

```yaml
---
- name: Show clock on Cisco devices
  hosts: cisco
  gather_facts: no

  tasks:
    - name: Run show clock
      cisco.ios.ios_command:
        commands:
          - show clock
      register: show_clock_output

    - name: Display output
      debug:
        msg: "{{ show_clock_output.stdout[0] }}"
```

## Prerequisites

Save both files in the same directory.

```text
ansible-lab/
├── inventory.yml
└── show_clock.yml
```

## Run the Playbook

```bash
ansible-playbook -i inventory.yml show_clock.yml -k
```

## Example Output

```text
PLAY [Show clock on Cisco devices] ********************************

TASK [Run show clock] *********************************************
ok: [192.168.1.10]

TASK [Display output] *********************************************
ok: [192.168.1.10] => {
    "show_clock_output.stdout_lines": [
        [
            "*10:15:32.123 UTC Mon Aug 18 2026"
        ]
    ]
}

PLAY RECAP *******************************************************
192.168.1.10 : ok=2 changed=0 unreachable=0 failed=0
```

## Benefits of Using a Playbook

- Reusable and easier to maintain.
- Can execute multiple commands in a single task.
- Easy to store in GitHub and version control.
- Provides a foundation for larger network automation workflows.
