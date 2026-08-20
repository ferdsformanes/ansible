# VS Code + WSL + Ansible Quick Guide

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

## 2. Open a WSL Terminal

In VS Code:

```text
Terminal -> New Terminal
```

Verify you are in WSL:

```bash
pwd
```

Example:

```text
/home/ferds
```

---

## 3. Go to the Ansible Directory

Run:

```bash
cd ~/ansible
```

Verify:

```bash
pwd
```

Expected output:

```text
/home/ferds/ansible
```

---

## 4. Verify the Files

Run:

```bash
ls
```

Example:

```text
ansible.cfg
gather_cisco_facts.yml
inventory.yml
show_clock.yml
```

---

## 5. Verify Ansible is Using ansible.cfg

Run:

```bash
ansible --version
```

Look for:

```text
config file = /home/ferds/ansible/ansible.cfg
```

If you see this line, Ansible is successfully reading your configuration file.

---

## 6. Verify Custom Configuration

Run:

```bash
ansible-config dump --only-changed
```

Example:

```text
CONFIG_FILE() = /home/ferds/ansible/ansible.cfg
DEFAULT_HOST_LIST(/home/ferds/ansible/ansible.cfg) = ['/home/ferds/ansible/inventory.yml']
HOST_KEY_CHECKING(/home/ferds/ansible/ansible.cfg) = False
PERSISTENT_COMMAND_TIMEOUT(/home/ferds/ansible/ansible.cfg) = 60
PERSISTENT_CONNECT_TIMEOUT(/home/ferds/ansible/ansible.cfg) = 60
```

---

## 7. Test the Inventory

Run:

```bash
ansible-inventory --list
```

Because the inventory is defined in `ansible.cfg`, you do not need:

```bash
-i inventory.yml
```

---

## 8. Run a Playbook

Example:

```bash
ansible-playbook show_clock.yml -k
```

Since `inventory.yml` is defined in `ansible.cfg`, there is no need to specify:

```bash
-i inventory.yml
```

---

## Directory Summary

```text
/home/ferds/ansible
├── ansible.cfg
├── inventory.yml
├── gather_cisco_facts.yml
└── show_clock.yml
```

### Purpose of Each File

- `ansible.cfg` = Ansible configuration settings
- `inventory.yml` = Device inventory
- `show_clock.yml` = Playbook to run show clock
- `gather_cisco_facts.yml` = Playbook to gather Cisco facts
