# Ansible Command Cheatsheet

## Quick Checks

### Show Ansible Version

```bash
ansible --version
```

Displays the installed Ansible version, Python version, configuration file in use, module search paths, collection locations, and executable location.

### Show Active Configuration

```bash
ansible-config dump
```

Displays the current configuration values that Ansible is actively using after applying defaults, environment variables, and configuration files.

### List Available Configuration Options

```bash
ansible-config list
```

Displays all configurable Ansible settings along with their descriptions, default values, environment variables, and configuration file options.

---

## Inventory Commands

### View inventory as JSON

```bash
ansible-inventory -i inventory.yml --list
```

Displays the complete inventory structure.

### View inventory as a tree

```bash
ansible-inventory -i inventory.yml --graph
```

Displays hosts and groups in a tree format.

### Show hosts matched by a pattern

```bash
ansible cisco -i inventory.yml --list-hosts
```

Shows which hosts will be targeted.

---

## Ad Hoc Commands

### Test connectivity

```bash
ansible all -i inventory.yml -m ping
```

Tests connectivity to managed hosts.

### Run a Cisco command

```bash
ansible cisco -i inventory.yml -m cisco.ios.ios_command -a "commands='show clock'" -k
```

Runs a Cisco IOS command.

### Gather Cisco facts

```bash
ansible cisco -i inventory.yml -m cisco.ios.ios_facts -k
```

Collects facts from Cisco devices.

---

## Playbook Commands

### Run a playbook

```bash
ansible-playbook -i inventory.yml show_clock.yml -k
```

Executes a playbook.

### Syntax check

```bash
ansible-playbook --syntax-check -i inventory.yml show_clock.yml
```

Validates playbook syntax without running it.

### Dry run

```bash
ansible-playbook --check -i inventory.yml show_clock.yml
```

Shows what changes would occur without making them.

### Verbose troubleshooting

```bash
ansible-playbook -i inventory.yml show_clock.yml -vvv
```

Displays detailed troubleshooting output.
