# Ansible Command Cheatsheet

## Quick Checks

```bash
ansible --version
ansible-config dump
ansible-config list
```

---

## Inventory Commands

### View inventory as JSON

```bash
ansible-inventory -i inventory.yml --list
```

### View inventory as a tree

```bash
ansible-inventory -i inventory.yml --graph
```

### Show hosts matched by a pattern

```bash
ansible cisco -i inventory.yml --list-hosts
```

---

## Ad Hoc Commands

### Test connectivity

```bash
ansible all -i inventory.yml -m ping
```

### Run a Cisco command

```bash
ansible cisco -i inventory.yml -m cisco.ios.ios_command -a "commands='show clock'" -k
```

### Gather Cisco facts

```bash
ansible cisco -i inventory.yml -m cisco.ios.ios_facts -k
```

---

## Playbook Commands

### Run a playbook

```bash
ansible-playbook -i inventory.yml show_clock.yml -k
```

### Syntax check

```bash
ansible-playbook --syntax-check -i inventory.yml show_clock.yml
```

### Dry run

```bash
ansible-playbook --check -i inventory.yml show_clock.yml
```

### Verbose troubleshooting

```bash
ansible-playbook -i inventory.yml show_clock.yml -vvv
```

---

## Collection Commands

### List installed collections

```bash
ansible-galaxy collection list
```

### Verify a collection

```bash
ansible-galaxy collection list cisco.ios
```

### Install a collection

```bash
ansible-galaxy collection install cisco.ios
```

### Upgrade a collection

```bash
ansible-galaxy collection install cisco.ios --force
```

---

## Documentation Commands

### List all modules

```bash
ansible-doc -l
```

### List Cisco IOS modules

```bash
ansible-doc -l | grep '^cisco\.ios'
```

### Module documentation

```bash
ansible-doc cisco.ios.ios_command
```

---

## Plugin Discovery

### Inventory plugins

```bash
ansible-doc -t inventory -l
```

### Connection plugins

```bash
ansible-doc -t connection -l
```

### Callback plugins

```bash
ansible-doc -t callback -l
```

---

## Collection Paths

```bash
ansible-config dump | grep COLLECTIONS_PATHS
```

---

## Daily-Use Commands

```bash
ansible --version
ansible-inventory -i inventory.yml --graph
ansible-inventory -i inventory.yml --list
ansible-galaxy collection list
ansible-doc -l | grep '^cisco\.ios'
ansible-doc cisco.ios.ios_command
ansible-playbook --syntax-check -i inventory.yml show_clock.yml
ansible-playbook -i inventory.yml show_clock.yml -k
ansible-playbook -i inventory.yml show_clock.yml -vvv
```
