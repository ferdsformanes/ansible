# Ansible Playbook - Show Clock

This guide demonstrates how to convert an Ansible ad hoc command into a reusable playbook.

## Original Ad Hoc Command

```bash
ansible cisco -i inventory.yml -m cisco.ios.ios_command -a "commands='show clock'" -k
```

## Inventory File

**inventory.yml**

```yaml
all:
  children:
    cisco:
      hosts:
        10.76.56.132:
      vars:
        ansible_connection: network_cli
        ansible_network_os: cisco.ios.ios
        ansible_user: formanesf-adm
```

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
        var: show_clock_output.stdout_lines
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
ok: [10.76.56.132]

TASK [Display output] *********************************************
ok: [10.76.56.132] => {
    "show_clock_output.stdout_lines": [
        [
            "*10:15:32.123 UTC Mon Aug 18 2026"
        ]
    ]
}

PLAY RECAP *******************************************************
10.76.56.132 : ok=2 changed=0 unreachable=0 failed=0
```

## Benefits of Using a Playbook

- Reusable and easier to maintain.
- Can execute multiple commands in a single task.
- Easy to store in GitHub and version control.
- Provides a foundation for larger network automation workflows.
