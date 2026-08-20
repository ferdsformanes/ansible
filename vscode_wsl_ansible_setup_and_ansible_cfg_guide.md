# VS Code WSL and ansible.cfg Setup Guide

## 1. Connect VS Code to WSL

Open VS Code.

Press:

```text
Ctrl + Shift + P
```

Type:

```text
WSL: Connect to WSL
```

or:

```text
WSL: Reopen Folder in WSL
```

You should see:

```text
[WSL: Ubuntu-24.04]
```

in the VS Code title bar and bottom-left corner.

---

## 2. Open the Ansible Folder

Open the folder:

```text
/home/ferds/ansible
```

---

## 3. Open a WSL Terminal

```bash
pwd
```

Expected output:

```text
/home/ferds/ansible
```

---

## 4. Create and Configure ansible.cfg

File: `ansible.cfg`

```ini
[defaults]
inventory = inventory.yml
host_key_checking = False

[persistent_connection]
connect_timeout = 60
command_timeout = 60
connect_retry_timeout = 30
```

### Explanation

- `inventory = inventory.yml` : Uses `inventory.yml` as the default inventory.
- `host_key_checking = False` : Disables SSH host key verification.
- `connect_timeout = 60` : Wait up to 60 seconds to establish a connection.
- `command_timeout = 60` : Wait up to 60 seconds for commands to complete.
- `connect_retry_timeout = 30` : Wait up to 30 seconds when connecting to the persistent connection socket.

---

## 5. Verify Ansible is Using ansible.cfg

```bash
ansible --version
```

Look for:

```text
config file = /home/ferds/ansible/ansible.cfg
```

---

## 6. Verify Custom Settings

```bash
ansible-config dump --only-changed
```

---

## 7. Verify the Inventory

```bash
ansible-inventory --list
```

---

## 8. Run a Playbook

```bash
ansible-playbook show_clock.yml -k
```

---

## Directory Structure

```text
/home/ferds/ansible
├── ansible.cfg
├── inventory.yml
├── gather_cisco_facts.yml
└── show_clock.yml
```
