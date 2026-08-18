# Ansible Ad Hoc Command - Show Clock

This ad hoc Ansible command connects to all hosts in the `cisco` group defined in `inventory.yml` and executes the Cisco IOS command `show clock`.

## Inventory File

**inventory.yml**

```yaml
all:
  children:
    cisco:
      hosts:
        192.168.1.10:   # Replace with your target device IP address
      vars:
        ansible_connection: network_cli
        ansible_network_os: cisco.ios.ios
        ansible_user: your_username   # Replace with your actual username
```

> **Note:** Replace `192.168.1.10` with the actual IP address of your Cisco device and replace `your_username` with your login username.

## Prerequisites

Save `inventory.yml` in the same directory where you will run the Ansible command.

Example:

```text
ansible-lab/
├── inventory.yml
```

From that directory, run:

```bash
ansible cisco -i inventory.yml -m cisco.ios.ios_command -a "commands='show clock'" -k
```

If `inventory.yml` is stored in a different location, update the `-i` parameter to point to the correct path.

Example:

```bash
ansible cisco -i /path/to/inventory.yml -m cisco.ios.ios_command -a "commands='show clock'" -k
```

## Command

```bash
ansible cisco -i inventory.yml -m cisco.ios.ios_command -a "commands='show clock'" -k
```

## Explanation

- `ansible cisco`
  - Targets all devices in the `cisco` inventory group.

- `-i inventory.yml`
  - Uses the YAML inventory file.

- `-m cisco.ios.ios_command`
  - Uses the Cisco IOS command module.

- `-a "commands='show clock'"`
  - Executes the `show clock` command on the device.

- `-k`
  - Prompts for the SSH password.

## Example Output

```text
192.168.1.10 | SUCCESS => {
    "changed": false,
    "stdout": [
        "*10:15:32.123 UTC Mon Aug 18 2026"
    ]
}
```
