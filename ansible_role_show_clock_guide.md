# Ansible Role Conversion Guide

## Original Playbook

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

## Project Structure

```text
project/
├── inventory.yml
├── show_clock.yml
└── roles/
    └── show_clock/
        ├── tasks/
        │   └── main.yml
        └── defaults/
            └── main.yml
```

## Playbook: `show_clock.yml`

```yaml
---
- name: Show clock on Cisco devices
  hosts: cisco
  gather_facts: no

  roles:
    - show_clock
```

## Role Task File: `roles/show_clock/tasks/main.yml`

```yaml
---
- name: Run show clock
  cisco.ios.ios_command:
    commands:
      - show clock
  register: show_clock_output

- name: Display output
  debug:
    msg: "{{ show_clock_output.stdout[0] }}"
```

## Run the Playbook

```bash
ansible-playbook -i inventory.yml show_clock.yml -k
```

## Recommended Filenames

- Playbook: `show_clock.yml`
- Role name: `show_clock`
- Role task file: `roles/show_clock/tasks/main.yml`

## Why Use Roles?

Roles become more useful when you start grouping multiple tasks, variables, templates, handlers, and files together.

```text
roles/
└── cisco_facts/
└── show_clock/
└── show_version/
└── interface_audit/
└── backup_config/
```

This keeps your playbooks clean:

```yaml
---
- name: Network validation
  hosts: cisco
  gather_facts: no

  roles:
    - show_clock
    - show_version
    - interface_audit
```
